# DB 5

## A Many-To-many-Relationship  + plus

M:N

- 한 테이블의 0개 이상의 레코드가 다른 테이블의 0개 이상의 레코드와 관련된 경우
- 양쪽 모두에서 N:1 관계를 가진다.

```python
from django.db import models

# Create your models here.
class Doctor(models.Model):
    name = models.TextField()

    def __str__(self):
        return f"{self.name} 전문의"
    
class Patient(models.Model):
    name = models.TextField()

    # doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
    name = models.TextField()
    def __str__(self):
        return f"{self.pk}번 환자 {self.name}"

class Reservation(models.Model):
    doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
    patient = models.ForeignKey(Patient, on_delete=models.CASCADE)
    def __str__(self):
        return f"{self.doctor_id}번의 의사의 {self.patient_id}번 환자"
```

- shell_plus

```jsx
In [1]: doctor1 = Doctor.objects.create(name='alice')

In [2]: patient1 = Patient.objects.create(name='carol')

In [3]: Reservation.objects.create(doctor=doctor1, patient=patient1)
Out[3]: <Reservation: 1번의 의사의 1번 환자>

In [4]: doctor1.reservation_set.all()
Out[4]: <QuerySet [<Reservation: 1번의 의사의 1번 환자>]>

In [5]: patient1.reservation_set.all()
Out[5]: <QuerySet [<Reservation: 1번의 의사의 1번 환자>]>
```

다른 방법으로 표현해보기

manytomanyfiled()

```python
from django.db import models

# Create your models here.
class Doctor(models.Model):
    name = models.TextField()

    def __str__(self):
        return f"{self.name} 전문의"
    
class Patient(models.Model):
    doctors = models.ManyToManyField(Doctor)
    name = models.TextField()

    # doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
    name = models.TextField()
    def __str__(self):
        return f"{self.pk}번 환자 {self.name}"
```

- shell_plus

```jsx
In [1]: doctor1 = Doctor.objects.create(name='alice')

In [2]: patient1 = Patient.objects.create(name='carol')

In [3]: patient2 = Patient.objects.create(name='doen')

In [4]: patient1.doctors.add(doctor1)

In [5]: patient1.doctors.all()
Out[5]: <QuerySet [<Doctor: alice 전문의>]>

In [6]: doctor1.patient_set.all()
Out[6]: <QuerySet [<Patient: 1번 환자 carol>]>
```

through를 통해서 만들어보자

```python
from django.db import models

# Create your models here.
class Doctor(models.Model):
    name = models.TextField()

    def __str__(self):
        return f"{self.name} 전문의"
    
class Patient(models.Model):
    doctors = models.ManyToManyField(Doctor, through='Reservation')
    name = models.TextField()

    # doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
    name = models.TextField()
    def __str__(self):
        return f"{self.pk}번 환자 {self.name}"

class Reservation(models.Model):
    doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
    patient = models.ForeignKey(Patient, on_delete=models.CASCADE)
    symptom = models.TextField()
    reserved_at = models.DateTimeField(auto_now_add=True)
    def __str__(self):
        return f"{self.doctor.pk}번의 의사의 {self.patient.pk}번 환자"
```

```jsx
In [1]: doctor1 = Doctor.objects.create(name='alice')

In [2]: patient1 = Patient.objects.create(name='carol')

In [3]: patient2 = Patient.objects.create(name='doen')

In [4]: reservation1 = Reservation(doctor=doctor1, patient=patient1, symptom='headache')

In [5]: reservation1.save()

In [6]: doctor1.patient_set.all()
Out[6]: <QuerySet [<Patient: 1번 환자 carol>]>

In [7]: patient1.doctors.all()
Out[7]: <QuerySet [<Doctor: alice 전문의>]>

In [8]: patient2.doctors.add(doctor1, through_defaults={'symptom': 'flu'})

In [9]: doctor1.patient_set.all()
Out[9]: <QuerySet [<Patient: 1번 환자 carol>, <Patient: 2번 환자 doen>]>

In [10]: patient2.doctors.all()
Out[10]: <QuerySet [<Doctor: alice 전문의>]>

예약 삭제
In [11]: doctor1.patient_set.remove(patient1)

In [12]: doctor1.patient_set.all()
Out[12]: <QuerySet [<Patient: 2번 환자 doen>]>
```