В цій лабораторній роботі необхідно зчитати WEB сторінку з сайту IMDB.com зі 100 фільмами 2017 року виходу за посиланням «http://www.imdb.com/search/title?count=100&release_date=2017,2017&title_type=feature».  Необхідно створити data.frame «movies» з наступними даними: номер фільму (rank_data), назва фільму (title_data), тривалість (runtime_data). Для виконання лабораторної рекомендується використати бібліотеку «rvest». CSS селектори для зчитування необхідних даних: rank_data: «.text-primary», title_data: «.lister-item-header a», runtime_data: «.text-muted .runtime». Для зчитування url використовується функція read_html, для зчитування даних по CSS селектору – html_nodes і для перетворення зчитаних html даних в текст - html_text. Рекомендується перетворити rank_data та runtime_data з тексту в числові значення. При формуванні дата фрейму функцією data.frame рекомендується використати параметр «stringsAsFactors = FALSE».

```r
imdb <- read_html('http://www.imdb.com/search/title?count=100&release_date=2017,2017&title_type=feature')
#ranks
> rank_data_html <- html_nodes(imdb,'.text-primary')
> rank_data <- as.numeric(html_text(rank_data_html))
> head(rank_data)
[1] 1 2 3 4 5 6

#titles
> title_data_html <- html_nodes(imdb, '.lister-item-header a')
> title_data <- html_text(title_data_html)
> head(title_data)
[1] "Зорянi вiйни: Останнi Джедаi"   "The Disaster Artist"           
[3] "The Shape of Water"             "Лiга справедливостi"           
[5] "Jumanji: Welcome to the Jungle" "Тор: Рагнарок" 

#runtime
> runtime_data_html <- html_nodes(imdb,'.text-muted .runtime')
> runtime_data <- html_text(runtime_data_html)
> head(runtime_data)
[1] "152 min" "104 min" "123 min" "120 min" "119 min" "130 min"
> runtime_data <- gsub(" min", "", runtime_data)
> runtime_data<-as.numeric(runtime_data)
> head(runtime_data)
[1] 152 104 123 120 119 130
> movies <- data.frame(Rank = rank_data, Title = title_data, Runtime = runtime_data, stringsAsFactors = FALSE)
> head(movies)
  Rank                          Title Runtime
1    1   Зорянi вiйни: Останнi Джедаi     152
2    2            The Disaster Artist     104
3    3             The Shape of Water     123
4    4            Лiга справедливостi     120
5    5 Jumanji: Welcome to the Jungle     119
6    6                  Тор: Рагнарок     130
```
 



1.	Виведіть перші 6 назв фільмів дата фрейму.

	```r
	> head(movies$Title)
	[1] "Зорянi вiйни: Останнi Джедаi"   "The Disaster Artist"           
	[3] "The Shape of Water"             "Лiга справедливостi"           
	[5] "Jumanji: Welcome to the Jungle" "Тор: Рагнарок" 
	```
2.	Виведіть всі назви фільмів с тривалістю більше 120 хв.

	```r
	> subset(movies, movies$Runtime > 120)$Title
	 [1] "Зорянi вiйни: Останнi Джедаi"            
	 [2] "The Shape of Water"                      
	 [3] "Тор: Рагнарок"                           
	 [4] "Mother!"                                 
	 [5] "Kingsman: Золоте кiльце"                 
	 [6] "Вартовi Галактики 2"                     
	 [7] "Воно"                                    
	 [8] "The Killing of a Sacred Deer"            
	 [9] "Darkest Hour"                            
	[10] "Call Me by Your Name"                    
	[11] "Той, хто бiжить по лезу 2049"            
	[12] "Валерiан i мiсто тисячi планет"          
	[13] "Логан: Росомаха"                         
	[14] "Phantom Thread"                          
	[15] "Downsizing"                              
	[16] "Диво-Жiнка"                              
	[17] "Людина-павук: Повернення додому"         
	[18] "Detroit"                                 
	[19] "All the Money in the World"              
	[20] "Molly's Game"                            
	[21] "Сiм сестер"                              
	[22] "Красуня i Чудовисько"                    
	[23] "Вiйна за планету мавп"                   
	[24] "Mudbound"                                
	[25] "The Square"                              
	[26] "Roman J. Israel, Esq."                   
	[27] "Пiрати Карибського моря: Помста Салазара"
	[28] "Трансформери: Останнiй лицар"            
	[29] "Пострiл в безодню"                       
	[30] "Power Rangers"                           
	[31] "Hostiles"                                
	[32] "Girls Trip"                              
	[33] "Джон Уiк 2" 
	```
3.	Скільки фільмів мають тривалість менше 100 хв.

	```r
	> nrow(subset(movies, movies$Runtime < 100))
	[1] 20
	```