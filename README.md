# Отток клиентов из банка
Из «Бета-Банка» стали уходить клиенты. Каждый месяц. Немного, но заметно. Банковские маркетологи посчитали: сохранять текущих клиентов дешевле, чем привлекать новых.

**Цель**: спрогнозировать, уйдёт клиент из банка в ближайшее время или нет. Предоставлены исторические данные о поведении клиентов и расторжении договоров с банком. 

Необходимо построить модель с предельно большим значением *F1*-меры. Успехом можно считать метрику более 0.59. Дополнительно измерим *AUC-ROC*, сравнивая значение с *F1*-мерой.

В ходе исследования были выполнены следуюшие шаги: 
* Загрузка и подготвка данных.
* Исследование баланса классов, обучение модели без учёта дисбаланса.
* Улучшение качества модели, учитывая дисбаланс классов. Обучение разных моделей.
* Финальное тестирование.

## Вывод

На этапе подготовки данных было принято решение обучать модели на данных с *удаленными пропусками*, а затем повторить исследование для лучшей модели на данных, в которых пропуски выделены в *отдельную категорию*. 

На этапе изучения модели без учёта дисбаланса классов у модели `RandomForestClassifier` f1 равен *0.6081*. Этот результат удалось улучшить *методом увеличения выборки* до *0.6231*.

Дополнительно были испробованы модели *DecisionTreeClassifier* и *LogisticRegression*, но их показатели оказались неудовлетворительными.

Лучшая модель по результатам исследования `RandomForestClassifier` обученная на увеличенной выборке с гиперпараметрами est=90, depth=10 на тестовой выборке показала f1 score **0.5943**, roc_auc_score **0.8489**, таким образом цель исследования в **59%** достигнута.

Дополнительное исследование для модели `RandomForestClassifier` было проведено на данных, в которых пропуски выделены в отдельную категорию.
На тесте по результатам этого исследования модель обученная на увеличенной выборке с гиперпараметрами est=90, depth=10: f1 score равен **0.6206**, roc_auc_score **0.8703**.

Таким образом, цель достигнута дважды. Лучший результат на данных с заполненными пропусками.
***
