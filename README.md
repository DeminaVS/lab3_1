# lab3_1
# Цель
Освоить основные приемы работы со строками и списками в
Python, изучить их встроенные методы и научиться применять их для решения
практических задач по обработке текстовой и структурированной информации.
# 3.1.1 Напишите функцию, которая принимает строку и возвращает её в перевернутом виде, не используя циклы.
```
def reverse_string(s):
    
    return s[::-1]

input_string = input()
reverse_str = reverse_string(input_string)
print(f"Перевернутая строка: {reverse_str}")
```
# 3.1.2 Напишите функцию, которая извлекает доменное имя из адреса электронной почты.
```
def get_email_domain(email):
    if '@' not in email:
        raise ValueError("Некорректный email адрес.")
    parts = email.split('@')
    domain = parts[1]
    
    return domain
try:
    email_address = input()
    domain = get_email_domain(email_address)
    print(f"Домен: {domain}")
except ValueError as e:
    print(f"Ошибка: {e}")
```
# 3.1.3 Напишите функцию для подсчета количества слов в предложении. Cлова разделены одним или несколькими пробелами. Знаки препинания не учитывать.
```
def count_words(sentence):
    for char in ".,!?;:-":
        sentence = sentence.replace(char, ' ')
    
    words = sentence.split()
    
    count = 0
    for word in words:
        if word.isalpha():  
            count += 1
    
    return count

text = input()
word_count = count_words(text)
print(f"Количество слов: {word_count}")
```
# 3.1.4 Напишите функцию, которая принимает список и возвращает новый список, содержащий только уникальные элементы из исходного.
```
def get_unique_elements(input_list):
    """Вернуть список с уникальными элементами из 'input_list' с сохранением порядка."""

    unique_list = []
    for item in input_list:
        if item not in unique_list:
            unique_list.append(item)
    return unique_list

input_str = input()
my_list = input_str.split()
unique_list = get_unique_elements(my_list)
print(f"Уникальные элементы: {unique_list}")
```
# 3.1.5 Напишите функцию, которая проверяет, является ли строка палиндромом (читается одинаково в обоих направлениях), игнорируя регистр и пробелы.
```
def is_palindrome(s):
    cleaned = ''.join(s.lower().split())
    return cleaned == cleaned[::-1]

text = input("Введите строку для проверки: ")
result = is_palindrome(text)

if result:
    print("Эта строка является палиндромом")
else:
    print("Эта строка не является палиндромом")
```
# 3.1.6 В компании принят формат кода товара: три буквы, дефис, три цифры, дефис, две буквы (например, XYZ-123-AB). Напишите функцию, которая форматирует строку вида xyz123ab в нужный формат.
```
def format_product_code(code):

    if len(code) != 8:
        raise ValueError(f"Неверная длина кода (требуется 8 символов).")
    part1 = code[:3]  
    part2 = code[3:6] 
    part3 = code[6:]  
    
    return f"{part1.upper()}-{part2}-{part3.upper()}"


try:
    product_code = input()
    formatted_code = format_product_code(product_code)
    print(f"Отформатированный код: {formatted_code}")
except ValueError as e:
    print(f"Ошибка: {e}")
```
# 3.1.7 Напишите функцию, которая принимает список чисел и возвращает их среднее арифметическое.
```
def calculate_average(numbers):
    if len(numbers) == 0:
        raise ZeroDivisionError("Список пуст")
    return sum(numbers) / len(numbers)


try:
    input_str = input()
    num_list = [float(x) for x in input_str.split()]
    average = calculate_average(num_list)
    print(f"Среднее арифметическое: {average:.2f}")
    
except ValueError:
    print("Ошибка: Введены нечисловые данные.")
except ZeroDivisionError:
    print("Ошибка: Нельзя вычислить среднее для пустого списка.")
```
# 3.1.8 Напишите функцию, которая принимает текст и список "стоп-слов". Функция должна заменять все стоп-слова в тексте на символ *.
```
def censor_text(text, stop_words):
    words = text.split()
    result_words = []
    for word in words:
        clean_word = word.strip('.,!?;:()-"\'')
        
        if clean_word.lower() in [stop_word.lower() for stop_word in stop_words]:
            result_words.append('*')
        else:
            result_words.append(word)
    return ' '.join(result_words)

text_to_censor = input()
stop_words_str = input()
stop_list = [word.strip() for word in stop_words_str.split(',')]
censored_text = censor_text(text_to_censor, stop_list)
print(f"Результат: {censored_text}")
```
# 3.1.9 Напишите функцию для генерации корпоративного email-адреса. Она должна принимать имя и фамилию, преобразовывать их в формат i.ivanov@company.com.
```
translit_map = {
    'а': 'a', 'б': 'b', 'в': 'v', 'г': 'g', 'д': 'd', 'е': 'e', 'ё': 'e', 'ж': 'zh',
    'з': 'z', 'и': 'i', 'й': 'y', 'к': 'k', 'л': 'l', 'м': 'm', 'н': 'n', 'о': 'o',
    'п': 'p', 'р': 'r', 'с': 's', 'т': 't', 'у': 'u', 'ф': 'f', 'х': 'h', 'ц': 'ts',
    'ч': 'ch', 'ш': 'sh', 'щ': 'sch', 'ъ': '', 'ы': 'y', 'ь': '', 'э': 'e', 'ю': 'yu', 'я': 'ya'
}

def transliterate(text):
    result = ""
    for char in text:
        if char.lower() in translit_map:
            if char.isupper():
                result += translit_map[char.lower()].capitalize()
            else:
                result += translit_map[char.lower()]
        else:
            result += char
    return result

def generate_corporate_email(first_name, last_name):
    if not first_name.strip() or not last_name.strip():
        raise ValueError("Имя и фамилия не могут быть пустыми.")
    first_latin = transliterate(first_name.strip().lower())
    last_latin = transliterate(last_name.strip().lower())
    first_initial = first_latin[0]
    return f"{first_initial}.{last_latin}@company.com"


try:
    first = input()
    last = input()
    email = generate_corporate_email(first, last)
    print(f"Корпоративный email: {email}")
except ValueError as e:
    print(f"Ошибка: {e}")
```
# 3.1.10 Напишите функцию, которая принимает список строк и возвращает новый список, содержащий только те строки, длина которых больше 5 символов.
```
def filter_long_strings(strings):
    result = []
    for string in strings:
        if len(string) > 5:
            result.append(string)
    
    return result

input_str = input()

word_list = [word.strip() for word in input_str.split(',')]
filtered_list = filter_long_strings(word_list)

print(f"Отфильтрованный список: {filtered_list}")
```
# 3.1.11 Напишите функцию, которая создает акроним (аббревиатуру) из фразы. Например, из "Key Performance Indicator" должно получиться "KPI".
```
def create_acronym_advanced(phrase):
    words = phrase.split()
    acronym = ''
    
    for word in words:
        if '-' in word:
            parts = word.split('-')
            for part in parts:
                if part:  
                    acronym += part[0].upper()
        else:
            if word:
                acronym += word[0].upper()
    
    return acronym

input_phrase = input("Введите фразу: ")
acronym_result = create_acronym_advanced(input_phrase)
print(f"Акроним: {acronym_result}")
```
# 3.1.12 Напишите функцию для форматирования телефонного номера. Она должна принимать строку из 11 цифр (например, 89211234567) и возвращать ее в формате +7 (921) 123-45-67.
```
def format_phone_number(phone):
    if len(phone) != 11 or not phone.isdigit():
        raise ValueError("Номер должен состоять из 11 цифр")

    country_code = "+7"
    operator_code = phone[1:4]
    first_part = phone[4:7]
    second_part = phone[7:9]
    third_part = phone[9:11]

    return f"{country_code} ({operator_code}) {first_part}-{second_part}-{third_part}"

input_phone = input("Введите номер телефона (11 цифр): ")
formatted_phone = format_phone_number(input_phone)
print(f"Отформатированный номер: {formatted_phone}")
```
#  3.1.13 Напишите функцию, которая разбирает строку в формате CSV (CommaSeparated Values) и возвращает список ее полей.
```
def parse_csv_simple(csv_string):

    fields = []
    current_field = ""
    inside_quotes = False
    
    for char in csv_string:
        if char == '"':
            inside_quotes = not inside_quotes
        elif char == ',' and not inside_quotes:
            fields.append(current_field)
            current_field = ""
        else:
            current_field += char
    
    fields.append(current_field)
    return fields

input_csv = input("Введите CSV строку: ")
parsed_fields = parse_csv_simple(input_csv)
print(f"Поля: {parsed_fields}")
```
# 3.1.14 Напишите функцию, которая находит самое длинное слово в списке слов.
```
def find_longest_word(words):

    if not words:
        return ""
    
    longest_word = words[0]
    for word in words:
        if len(word) > len(longest_word):
            longest_word = word
    
    return longest_word

input_words = input("Введите слова через пробел: ")
words_list = input_words.split()

longest = find_longest_word(words_list)
print(f"Самое длинное слово: '{longest}' (длина: {len(longest)})")
```
# 3.1.15 В целях безопасности необходимо маскировать номера кредитных карт. Напишите функцию, которая принимает номер карты (строку из 16 цифр) и возвращает его в виде, где первые 12 цифр заменены на *.
```
def mask_credit_card(card_number):

    if len(card_number) != 16 or not card_number.isdigit():
        raise ValueError("Номер карты должен состоять из 16 цифр")
    masked = '*' * 12 + card_number[-4:]
    return masked

input_card = input("Введите номер карты (16 цифр): ")
masked_card = mask_credit_card(input_card)
print(f"Замаскированный номер: {masked_card}")
```
# 3.1.16 Напишите функцию, которая сортирует список полных имен ("Имя Фамилия") по фамилии.
```
def sort_by_surname(full_names):
    return sorted(full_names, key=lambda name: name.split()[-1])

print("Введите полные имена (каждое с новой строки, пустая строка - завершение):")
names_list = []
while True:
    name = input().strip()
    if not name:
        break
    names_list.append(name)

sorted_names = sort_by_surname(names_list)
print("\nОтсортированный список по фамилии:")
for name in sorted_names:
    print(name)
```
# 3.1.17 Напишите функцию, которая "сплющивает" вложенный список (список списков) в один плоский список.
```
def flatten_list(nested_list):
    result = []
    
    for item in nested_list:
        if isinstance(item, list):
            result.extend(flatten_list(item))
        else:
            result.append(item)
    
    return result

print("Введите вложенный список в формате: [1, [2, 3], 4, [5, [6, 7]]]")
try:
    input_list = eval(input("Введите список: "))
    if not isinstance(input_list, list):
        raise ValueError("Введенные данные не являются списком")
    
    flattened = flatten_list(input_list)
    print(f"Плоский список: {flattened}")
    
except:
    print("Ошибка: введите корректный список в формате Python")
```
# 3.1.18 Напишите функцию, которая удаляет все знаки препинания из текста.
```
def remove_punctuation_simple(text):

    punctuation = '!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'

    for char in punctuation:
        text = text.replace(char, '')
    
    return text

input_text = input("Введите текст: ")
cleaned_text = remove_punctuation_simple(input_text)
print(f"Текст без знаков препинания: {cleaned_text}")
```
# 3.1.19 Напишите функцию, которая объединяет два списка и возвращает новый отсортированный список без дубликатов.
```
def merge_and_sort_unique(list1, list2):

    unique_elements = set(list1 + list2)

    sorted_list = sorted(unique_elements)
    
    return sorted_list

print("Введите элементы первого списка через пробел:")
input_list1 = input().split()

print("Введите элементы второго списка через пробел:")
input_list2 = input().split()

try:
    list1 = [int(x) for x in input_list1]
    list2 = [int(x) for x in input_list2]
except ValueError:

    list1 = input_list1
    list2 = input_list2

result = merge_and_sort_unique(list1, list2)
print(f"Объединенный отсортированный список без дубликатов: {result}")
```
# 3.1.20 Напишите функцию, которая извлекает все хэштеги (слова, начинающиеся с #) из строки.
```
def extract_hashtags_simple(text):
    hashtags = []
    words = text.split()
    
    for word in words:
        if word.startswith('#') and len(word) > 1:
            clean_word = word.strip('.,!?;:()[]{}"\'')
            hashtags.append(clean_word)
    
    return hashtags

input_text = input("Введите текст с хэштегами: ")
hashtags_list = extract_hashtags_simple(input_text)

print(f"Найденные хэштеги: {hashtags_list}")
```
