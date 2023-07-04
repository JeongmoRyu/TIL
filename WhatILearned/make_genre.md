# Make Genre with python 

```python
import json
import requests

class TMDBHelper:
    def __init__(self, api_key=None):
        self.api_key = api_key
    def get_request_url(self, method='/movie/popular', **kwargs):
        base_url = 'https://api.themoviedb.org/3'
        request_url = base_url + method
        request_url += f'?api_key={self.api_key}'

        for k, v in kwargs.items():
            request_url += f'&{k}={v}'
        
        return request_url

def get_top_rated():
    result = []
    ranking = 0
    for page in range(1, 10):
        request_url = TMDBHelper.get_request_url(method='/movie/top_rated', region='KR', language='ko', page=f'{page}')
        raw_data = requests.get(request_url).json()
        data = raw_data.get('results')
        for movie in data:
            ranking += 1
            movie_dict = {
                "model" : "movies.movie",
                "pk" : movie.get("id"),
                "fields" : {
                    "title" : movie.get("title"),
                    "overview" : movie.get("overview"),
                    "popularity" : movie.get("popularity"),
                    "vote_count" : movie.get("vote_count"),
                    "release_data" : movie.get("release_data"),
                    "poster_path" : movie.get("poster_path"),
                    "genre_ids" : movie.get("genre_ids"),
                    "year" : int(movie.get("release_data")[:4]),
                    "ranking" : ranking,
                }
            }
            result.append(movie_dict)
    return result
with open('./fixtures/top_rated.json', 'w', encoding="UTF-8") as f:
    json.dump(get_top_rated(), f, ensure_ascii=False, indent=2)
```