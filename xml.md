import xml.etree.ElementTree as ET
from collections import Counter
def read_xml(file_path, word_max_len=6, top_words_amt=10):
    parser = ET.XMLParser(encoding='utf-8')
    tree = ET.parse('newsafr.xml', parser)
    root = tree.getroot()
    news_list = root.findall('channel/item')
    all_words = []
    descriptions = [item.find('description').text.split() for item in news_list]
    for description in descriptions:
        description = [word for word in description if len(word) > word_max_len]
        all_words.extend(description)
    words_counter = Counter(all_words)
    popular_words = [w[0] for w in words_counter.most_common(top_words_amt)]
    return popular_words

if __name__ == '__main__':
    print(read_xml('newsafr.xml'))