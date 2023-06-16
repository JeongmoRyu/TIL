# make_json_actor

import requests
import json

with open ("moviedata2.json", "r",  encoding='UTF-8') as f:
    data = json.load(f)

TMDB_API_KEY ='****************************'

def get_actor_datas(id):
    request_url = f"https://api.themoviedb.org/3/person/{id}?api_key={TMDB_API_KEY}&language=en-US"
    actor = requests.get(request_url).json()
    

    if actor.get('know_for_department', 'Acting'):
        fields = {
            'name': actor['name'],
            'profile_path': actor['profile_path'],
        }

        data = {
            "pk": id,
            "model": "movies.actor",
            "fields": fields
        }

        actor_list.append(data)



actor_list = []

detail_actor = []
for i in range(len(data)):
    for j in range(len(data[i]['fields']['actors'])):
        if data[i]['fields']['actors'][j] not in detail_actor:
            detail_actor.append(data[i]['fields']['actors'][j])

actor_num = len(detail_actor)
# print(actor_num)

for i in range(1447):
    get_actor_datas(detail_actor[i])


file_path = "./actor.json"
with open(file_path, 'w',  encoding='UTF-8') as outfile:
    json.dump(actor_list, outfile)