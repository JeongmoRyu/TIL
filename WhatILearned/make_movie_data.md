# make movie data

```python

import requests
import json


TMDB_API_KEY ='****************************'



def get_movie_datas():
    for i in range(1, 10):
        request_url = f"https://api.themoviedb.org/3/movie/popular?api_key={TMDB_API_KEY}&language=ko-KR&page={i}"

        movies = requests.get(request_url).json()
        for movie in movies['results']:
            if movie.get('title', ''):
                fields = {
                    'genres': movie['genre_ids'],
                    'title': movie['title'],
                    'overview': movie['overview'],
                    'popularity': movie['popularity'],
                    'poster_path': movie['poster_path'],
                    'release_date': movie.get('release_date'),
                    'vote_average': movie['vote_average'],
                    'vote_count': movie['vote_count'],
                    'video_key' : '',
                    'actors' : []
                }

                data = {
                    "pk": movie['id'],
                    "model": "movies.movie",
                    "fields": fields
                }

                movie_list.append(data)

    

def credits(title):

    base_url = 'https://api.themoviedb.org/3/search/movie?api_key=cec1ac30c15be1288013fffafcfe2c04&language=ko&'
    search_url = 'query='+ str(title) + '&include_adult=true'
    url = base_url + search_url
    url_result = requests.get(url).json()

    base_url_2 = 'https://api.themoviedb.org/3/movie/'
    search_url_2 = str(url_result['results'][0]['id']) + '/credits?api_key=cec1ac30c15be1288013fffafcfe2c04&language=ko&'
    url_2 = base_url_2 + search_url_2
    url_result_2 = requests.get(url_2).json()

    result_2 = []
    for i in range(len(url_result_2['cast'])) :
        if url_result_2['cast'][i]['known_for_department'] == "Acting":
            result_2.append(url_result_2['cast'][i]['id'])
        if len(result_2) >= 10:
            break

    
    return result_2


with open ("moviedata2.json", "r",  encoding='UTF-8') as f:
    data = json.load(f)

def get_video_datas(id):
    request_url = f"https://api.themoviedb.org/3/movie/{id}/videos?api_key={TMDB_API_KEY}&language=ko"
    video = requests.get(request_url).json()
    # print(video)
    # print(video['id'])
    # print(video['results'])
    if len(video["results"]) > 0:
        for i in range(len(video["results"])):
            if video['results'][i].get('type') =='Trailer':
            # print(f'{id}')
                fields = {
                    'video_key': video['results'][i]['key'],
                }
                data = {
                    "pk": id,
                    "model": "movies.video",
                    "fields": fields
                }
                video_list.append(data)
                break


video_list = []
videos = []
movie_list = []

get_movie_datas()


for i in range(len(data)):
    videos.append(data[i]['pk'])
# print(videos)

for i in range(len(videos)):
    get_video_datas(videos[i])


# print(movie_list)
# print(videos)
# print(video_list)

for i in range(len(movie_list)):
    # movie_list[i]['fields']['words'] = videos[i]['fields']['words']
    actor_list = credits(movie_list[i]['fields']['title'])
    movie_list[i]['fields']['actors'] = actor_list

for i in range(len(movie_list)):
    for j in range(len(video_list)):
        if movie_list[i]['pk'] == video_list[j]['pk']:
            movie_list[i]['fields']['video_key'] = video_list[j]['fields']['video_key']
        # if len(movie_list[i]['fields']['video_key']) == 0:
        #     movie_list[i]['fields']['video_key'] = ''


# print(movie_list)

file_path = "./moviedata_final.json"
with open(file_path, 'w',  encoding='UTF-8') as outfile:
    json.dump(movie_list, outfile, indent="\t", ensure_ascii=False)
```