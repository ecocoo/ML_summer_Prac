# Сравнение на MNIST
## Ход работы
- Были обучены три модели на наборе данных MNIST:
- - Полносвязная сеть (FCN) с тремя-четырьмя слоями
- - Простая CNN с двумя-тремя сверточными слоями 
- - CNN с остаточными блоками (ResNetCNN).
-  Все модели обучались с одинаковыми гиперпараметрами, включая размер батча 64 и 5 эпох. 
- Было измерено время обучения и инференса, а также собраны данные о точности на обучающей и тестовой выборках. 
- Были визуализированы кривые обучения для каждой модели, чтобы оценить динамику потерь и точности.
## Полученные графики и результаты 
![alt text]([images/image-12.png](https://github.com/ecocoo/ML_summer_Prac/blob/main/Lessons_4/HW/images/image-12.png))
![alt text]([images/image-13.png](https://github.com/ecocoo/ML_summer_Prac/blob/main/Lessons_4/HW/images/image-13.png))
![alt text]([images/image-14.png](https://github.com/ecocoo/ML_summer_Prac/blob/main/Lessons_4/HW/images/image-14.png))

### Сравнение моделей:

Model           Train Acc  Test Acc   Train Time (s)  Infer Time (s)  Params    
---------------------------------------------------------------------------
FCN             0.9792     0.9788     28.63           1.38            567434    
SimpleCNN       0.9919     0.9918     134.88          5.78            421642    
ResNetCNN       0.9930     0.9862     905.25          36.13           160906   

## Выводы
- Анализ показывает, что ResNetCNN достигла наивысшей точности на обучающей выборке (0.9930) 
- SimpleCNN также показала высокую точность (0.9919 на train и 0.9918 на test), близкую к ResNetCNN, но с меньшим временем обучения (134.88 с). 
- FCN, несмотря на меньшее время обучения (28.63 с) и инференса (1.38 с), имеет чуть меньшую точность (0.9788 на test)
- ResNetCNN, хотя и имеет наименьшее количество параметров (160,906), требует значительно больше времени (905.25 с на обучение и 36.13 с на инференс), это связано с дополнительной сложностью остаточных связей. 
- Кривые обучения демонстрируют стабильное снижение потерь и рост точности для всех моделей, с заметным преимуществом CNN-архитектур над FCN в итоговой производительности.



# Сравнение на CIFAR-10
## Ход работы
- Были обучены три модели на наборе данных CIFAR-10: 
- - Глубокая полносвязная сеть (FCN)
- - CNN с остаточными блоками (ResNetCNN)
- - CNN с остаточными блоками и регуляризацией (RegResNetCNN)
- Все модели обучались с одинаковыми гиперпараметрами (размер батча 64, 10 эпох) на устройстве MPS. 
- Были измерены точность на обучающей и тестовой выборках, время обучения и инференса, а также проанализировано переобучение. 
- Для каждой модели построены матрицы ошибок и исследованы средние значения градиентов по слоям.

## Полученные графики и результаты 
![alt text]([images/image-15.png](https://github.com/ecocoo/ML_summer_Prac/blob/main/Lessons_4/HW/images/image-15.png))
![alt text]([images/image-16.png](https://github.com/ecocoo/ML_summer_Prac/blob/main/Lessons_4/HW/images/image-16.png))
![alt text]([images/image-17.png](https://github.com/ecocoo/ML_summer_Prac/blob/main/Lessons_4/HW/images/image-17.png))
![alt text]([images/image-18.png](https://github.com/ecocoo/ML_summer_Prac/blob/main/Lessons_4/HW/images/image-18.png))
![alt text]([images/image-19.png](https://github.com/ecocoo/ML_summer_Prac/blob/main/Lessons_4/HW/images/image-19.png))
![alt text]([images/image-20.png](https://github.com/ecocoo/ML_summer_Prac/blob/main/Lessons_4/HW/images/image-20.png))
![alt text]([images/image-21.png](https://github.com/ecocoo/ML_summer_Prac/blob/main/Lessons_4/HW/images/image-21.png))
![alt text]([images/image-22.png](https://github.com/ecocoo/ML_summer_Prac/blob/main/Lessons_4/HW/images/image-22.png))
![alt text]([images/image-23.png](https://github.com/ecocoo/ML_summer_Prac/blob/main/Lessons_4/HW/images/image-23.png))

### Сравнение моделей на CIFAR-10:
Model           Train Acc  Test Acc   Overfit Gap  Train Time (s)  Infer Time (s)  Params    
-------------------------------------------------------------------------------------
FCN             0.6550     0.5106     0.1444       78.92           0.80            820874    
ResNetCNN       0.9037     0.8237     0.0800       334.96          2.20            161482    
RegResNetCNN    0.7456     0.7757     -0.0301      372.68          1.50            161482  

## Выводы
- Анализ показывает, что ResNetCNN достигла наивысшей точности на обучающей выборке (0.9037) и тестовой (0.8237), но с заметным разрывом переобучения (0.0800)
- FCN продемонстрировала наименьшую точность (0.5106 на тесте) и наименьшее время обучения (78.92 с), но с сильным переобучением (0.1444)
- RegResNetCNN с регуляризацией показала сбалансированную производительность (0.7757 на тесте) с отрицательным разрывом переобучения (-0.0301)
- Время обучения для ResNetCNN и RegResNetCNN значительно выше (334.96 с и 372.68 с ), но они эффективнее в извлечении признаков, как видно из матриц ошибок с более выраженной диагональю. 
- Градиенты для FCN показывают более выраженные колебания, тогда как у ResNetCNN и RegResNetCNN они более стабильны, что подтверждает пользу остаточных связей и регуляризации.
