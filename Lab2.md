1.	Створить список list1 <-  list(observationA = c(1:5, 7:3), observationB = matrix(1:6, nrow=2)). Для цього списку знайдіть sum за допомогою lapply.

	```r
	> list1 <-  list(observationA = c(1:5, 7:3), observationB = matrix(1:6, nrow=2))
	> list1
	$observationA
	 [1] 1 2 3 4 5 7 6 5 4 3
	
	$observationB
	     [,1] [,2] [,3]
	[1,]    1    3    5
	[2,]    2    4    6
	```
2.	Для кожного елементу списку list1 знайдіть максимальне та мінімальне значення (range) за допомогою lapply та sapply.

	```r
	> lapply(list1,min)
	$observationA
	[1] 1
	
	$observationB
	[1] 1
	
	> lapply(list1,max)
	$observationA
	[1] 7
	
	$observationB
	[1] 6
	
	> sapply(list1,min)
	observationA observationB 
	           1            1 
	> sapply(list1,max)
	observationA observationB 
	           7            6 
	```
3.	Для вбудованого набору даних InsectSprays знайти середнє count для кожного spray.

	```r
	> lapply(split(InsectSprays,InsectSprays$spray), function(x) mean(x$count))
	$A
	[1] 14.5
	
	$B
	[1] 15.33333
	
	$C
	[1] 2.083333
	
	$D
	[1] 4.916667
	
	$E
	[1] 3.5
	
	$F
	[1] 16.66667
	```
