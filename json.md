import json
from collections import Counter

def read_json(file_path, word_max_len=6, top_words_amt=10):
    with open (file_path, 'r', encoding='utf-8') as f:
        data = json.load(f)
        all_words = []
        for news in data['rss']['channel']['items']:
            total = [word for word in news['description'].split( ) if len(word) > word_max_len]
            all_words.extend(total)
        top_10 = Counter(all_words).most_common(top_words_amt)
        popular_words = [word[0] for word in top_10]
    return popular_words


if __name__ == '__main__':
    print(read_json('newsafr.json'))