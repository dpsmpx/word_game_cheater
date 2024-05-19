# this is the core
```python
def remove_symbol(word, symbol):
    # Используем срезы для удаления символа из слова
    return word[:word.find(symbol)] + word[word.find(symbol) + 1:]


def match(word, mask, ignoring):
    if len(word) != len(mask):
        return False
    else:
        for pos in range(len(word)):
            if mask[pos] != "*" and mask[pos] != word[pos] or word[pos] in ignoring:
                return False
    return True


def contains(g_word, word):
    # если подставляемое слово больше основного - игнор слова
    if len(word) > len(g_word):
        return False
    else:
        # ищем все буквы подставляемого слова в искомом и убираем когда находим, если не нашли совсем - игнор слова
        for pos in range(len(word)):
            if word[pos] not in g_word:
                return False
            else:
                g_word = remove_symbol(g_word, word[pos])
    return True


def search_words_by_mask(mask, ignoring):
    words = nouns

    # найти подходящие слова
    matches = []
    for word in words:
        if match(word, mask, ignoring):
            matches.append(word)

    # вернуть результат - подходящие слова
    return matches


def search_words_from_word(g_word):
    words = nouns

    # найти подходящие слова
    matches = []
    for word in words:
        if contains(g_word, word):
            matches.append(word)

    # вернуть результат - подходящие слова
    return matches


def words_by_mask():
    mask = input("Введите маску слова: ")
    ignoring = input("Введите запрещённые буквы: ")
    print("Слова, соответствующие маске:")
    for word in search_words_by_mask(mask, ignoring):
        print(word)


def words_from_word():
    g_word = input("Введите слово: ")
    print("Подходящие слова:")
    for word in search_words_from_word(g_word):
        print(word)


# меню
choice = int(input("0 - поиск по маске\n1 - слова из слова\n"))
if choice == 0:
    words_by_mask()
elif choice == 1:
    words_from_word()

# конец файла
```

# this is words formatter
```python
import os

def add_quotes(filename):
    with open(filename, 'r', encoding="utf8") as file:
        lines = file.readlines()
    
    with open(filename+"2.txt", 'w', encoding="utf8") as file:
        for line in lines:
            # Добавляем двойные кавычки в начало и конец строки, а также запятую после каждой строки
            file.write(f'"{line.strip()}",\n')

# Путь к файлу должен быть указан правильно
add_quotes("words.txt")
```
