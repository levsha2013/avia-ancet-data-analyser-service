# Pet project: analizer avia_data
### Данный проект был создан как выпускная работа курса ["Разработка ML сервиса: от идеи к прототипу"](https://stepik.org/course/176820/info) 

### Входные данные содержат следующие группы признаков:
- [X] характеристики пассажиров (Age, Gender, Type_of_Travel, ...)
- [X] оценки от пассажиров полета (Food and drink, Seat comfort, Cleanliness, ...)
- [X] целевая переменная - доволен пассажир перелетом или нет (satifaction)

### Для построения серсиса было проведено следующее:
- [X] обнаружение и устранение ошибок в данных (на основании их распределения)
- [X] статист. подтверждение обоснованности факторного анализа и непосредственно факторный анализ (осмысленное уменьшение размерности данных)
- [X] подбор гиперпараметров с помощью opruna для CatBoostClassifier по f1 метрике на GPU
- [X] написание сервиса на streamlit для взаимодействия с обученной моделью и данными

***Код каждого из шагов с комментариями находится в каталоге Jupyter***

![Пример отображения работающего сервиса](https://github.com/levsha2013/avia-ancet-data-analyser-service/blob/master/images/main_print.png)

### Для локального запуска проекта необходимо:
1. Скачать репозиторий.
2. Создать свое виртуальное окружение.
3. Активировать виртуальное окружение.
4. Установить все библиотеки, указанные в файле requirements.txt
5. Запустить проект через команду streamlit run Предсказание.py

## Результаты 

1. EDA и предобработкой данных получилось неплохо и качественно преобразовать данные. Однако не было обнаружено полезности признаков задержки прибытия и отправления - эти признаки не участвовали в дальнейшем преобразовании.
2. Проведенный факторный анализ превосходно себя показал! Из 14 признаков - оценок пассажиров выделено 4 фактора, которые к тому же были выделены однозначно
3. В качестве предсказания была использована модель логистической регрессии без гиперпараметров. Значение метрики ROC-AUG 0.85.
4. Для вывода значимости признаков для каждого предсказания используется модуль interpretation.py. В нем выделяется подмножество похожих пассажиров, производится обучение предсказания удовлетворенности клиентов (используется catboost) и выделяется feature_importance. 