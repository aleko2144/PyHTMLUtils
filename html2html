#Импорт встроенной библиотеки sys
import sys
#Импорт модуля HTMLParser из модуля parser встроенной библиотеки html
from html.parser import HTMLParser

#Массив для имён документов
names = []
#Массив для ссылок на документы
links = []

#Скопировано с https://docs.python.org/3.11/library/html.parser.html
#Класс-обработчик html-кода при помощи модуля HTMLParser
class MyHTMLParser(HTMLParser):
	#Срабатывает, если парсер нашёл открывающий тег
	def handle_starttag(self, tag, attrs):
		#Если открывающий тег = a, то тогда сохранение URL-ссылки в массив links
		if tag == "a":
			links.append(attrs[2][1])
		pass

	def handle_endtag(self, tag):
		pass

	#Выводит данные, расположенные между тегами - обычно это строковые подписи
	# по типу "Файл", "Б17Б Химия" и пр.
	def handle_data(self, data):
		#Проверка - если парсер нашёл строку длиной больше 5, то это вероятнее
		# всего имя дисциплины из списка
		if len(data) > 5: #чтобы пропустить "html", "Test", " Файл" и т.п.
			names.append(data)

def main():
	#Открытие исходного html-файла в переменную input
	input = open('_src.html','r', encoding="utf8")
	#Открытие выходного html-файла в переменную output
	output = open('_out.html','w')
	
	#Сохранение всех строк исходного html-файла в массив html_data
	html_data = input.readlines()
	
	#Создание экземпляра класса MyHTMLParser и передача ему
	# данных исходного файла
	parser = MyHTMLParser()
	parser.feed(html_data[0])
	
	#После работы парсера, сохранение 
	for i in range(len(names)):
		#Далее в файл записывается открывающий тег элемента списка - <li>
		output.write('<li>\n')
		#Запись ссылки во формате <a class=... href="ссылка">подпись</a>
		output.write('\t<a class="inline-link" href="{}">{}</a>\n'.format(links[i], names[i]))
		#И, наконец, закрывающий тег элемента - </li>
		output.write('</li>\n\n')

	#Закрытие файлов
	input.close()
	output.close()

	#Завершение программы
	sys.exit()

#Аналогично предыдущему парсеру
if __name__ == '__main__':
    main()
