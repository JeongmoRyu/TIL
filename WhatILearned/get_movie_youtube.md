# get movie youtube

import requests
import json

with open ("moviedata2.json", "r",  encoding='UTF-8') as f:
    data = json.load(f)

TMDB_API_KEY ='****************************'

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
                    'videoKey': video['results'][i]['key'],
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
for i in range(len(data)):
    videos.append(data[i]['pk'])
print(len(videos))

for i in range(len(videos)):
    get_video_datas(videos[i])

print(video_list)

# file_path = "./videodata.json"
# with open(file_path, 'w',  encoding='UTF-8') as outfile:
#     json.dump(video_list, outfile)