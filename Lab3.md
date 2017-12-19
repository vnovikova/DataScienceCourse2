1.	За допомогою download.file() завантажте любий excel файл з порталу http://data.gov.ua та зчитайте його (xls, xlsx – бінарні формати, тому встановить mode = “wb”. Виведіть перші 6 строк отриманого фрейму даних.
	
	```r
	> Sys.setlocale(locale = 'ukrainian')
	> download.file('http://data.gov.ua/file/153437/download?token=rBuYVHbP', 'data.xls')
	> data <- read.xlsx('data.xls', sheetIndex = 1, header = TRUE)
	> head(data)
	                                                                                                                                                                                                         NA.
	1 Реєстр документів, розпорядником яких є Управління житлово-комунального господарства, енергозбереження та паливно-енергетичного комплексу Сумської обласної державної адміністрації (станом на 15.12.2017)
	2                                                                                                                                                                                                       <NA>
	3                                                                                                                                                                                     Номер облікової картки
	4                                                                                                                                                                                                          1
	5                                                                                                                                                                                                          2
	6                                                                                                                                                                                                          3
	          NA..1                                                    NA..2                    NA..3      NA..4                        NA..5      NA..6
	1          <NA>                                                     <NA>                     <NA>       <NA>                         <NA>       <NA>
	2          <NA>                                                     <NA>                     <NA>       <NA>                         <NA>       <NA>
	3 Вид документа                                          Назва документа Дата створення документа      Номер                Ключові слова Тип, носій
	4          Лист про надання інформації про суб'єктів природних монополій                    43070 01-11/1697 суб'єкти природних монополій   Паперова
	5          Лист                                     про прийняття витрат                    43070 03-05/1698                      витрати   Паперова
	6          Лист                   щодо відключення від електропостачання                    43070 02-04/1699            електропостачання   Паперова
	                                NA..7            NA..8                       NA..9                          NA..10
	1                                <NA>             <NA>                        <NA>                            <NA>
	2                                <NA>             <NA>                        <NA>                            <NA>
	3                  Джерело інформації Місце зберігання Дата направлення до відділу                          Галузь
	4 Управління ЖКГЕ та ПЕК Сумської ОДА       Управління                       43070 житлово-комунальне господарство
	5 Управління ЖКГЕ та ПЕК Сумської ОДА       Управління                       43070 житлово-комунальне господарство
	6 Управління ЖКГЕ та ПЕК Сумської ОДА       Управління                       43070 житлово-комунальне господарство
	                                                  NA..11                  NA..12
	1                                                   <NA>                    <NA>
	2                                                   <NA>                    <NA>
	3 Підстава віднесення до інформації з обмеженим доступом Строк обмеження доступу
	4                                                      -                       -
	5                                                      -                       -
	6                                                      -                       -
	```
2.	За допомогою download.file() завантажте файл getdata_data_ss06hid.csv за посиланням https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv та завантажте дані в R. Code book, що пояснює значення змінних знаходиться за посиланням https://www.dropbox.com/s/dijv0rlwo4mryv5/PUMSDataDict06.pdf?dl=0  Необхідно знайти, скільки property мають value $1000000+

	```r
	> download.file('https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv', 'lab3_2.csv')
	trying URL 'https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv'
	Content type 'text/csv' length 4246554 bytes (4.0 MB)
	downloaded 4.0 MB
	
	> data <- read.csv('lab3_2.csv')
	> nrow(subset(data, data$VAL == 24))
	[1] 53
	```
3.	Зчитайте xml файл за посиланням http://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Frestaurants.xml Скільки ресторанів мають zipcode 21231?

	```r
	> file_xml <- xmlTreeParse('http://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Frestaurants.xml', useInternal=TRUE)
	> root <- xmlRoot(file_xml)
	> zipcodes <- xpathSApply(root, "//zipcode", xmlValue)
	> length(zipcodes[zipcodes == '21231'])
	[1] 127
	```