# Поиск вакансий и сотрудников

% есть база со скилами,вакансиями и статусом(уровнем соискателя)

```
skill(python).
skill(sql).
skill(js).
skill(english).
skill(excel).

vacancy(ds).
vacancy(marketolog).
vacancy(tester).

status(student).
status(junior).
status(middle).
status(senior).
```
% требования к соискателю и возможные ограничения для конкретных вакансий:
```
req(ds,Y,Z):-skill(Y),status(Z),(Y=python;Y=sql),not(Z=student;Z=junior).
req(marketolog,Y,Z):-skill(Y),status(Z),(Y=excel;Y=english).
req(tester,Y,Z):-skill(Y),status(Z),(Y=python,Y=sql),(Z=student;Z=junior).
```
% "рабочая" вакансия или объявление включает в себя название должности, навыки и требуемый уровень
```
work(V,C,D):-vacancy(V),skill(C),status(D),req(V,C,D).
```
% у соискателей также есть ряд своих признаков:
```
person(peter,Y,Z):-skill(Y),status(Z),(Y=python;Y=sql),(Z=middle).
person(mary,Y,Z):-skill(Y),status(Z),(Y=excel;Y=sql;Y=english),(Z=student).
person(kira,Y,Z):-skill(Y),status(Z),(Y=python;Y=sql;Y=english),(Z=junior).
```
% и сопоставляем работу и человека:
```
workman(N,V,C,D):-work(V,C,D),person(N,C,D).
```

% полный код
```
vacancy(ds).
vacancy(marketolog).
vacancy(tester).
skill(python).
skill(sql).
skill(js).
skill(english).
skill(excel).
status(student).
status(junior).
status(middle).
status(senior).

req(ds,Y,Z):-skill(Y),status(Z),(Y=python;Y=sql),not(Z=student;Z=junior).
req(marketolog,Y,Z):-skill(Y),status(Z),(Y=excel;Y=english).
req(tester,Y,Z):-skill(Y),status(Z),(Y=python,Y=sql),(Z=student;Z=junior).

work(V,C,D):-vacancy(V),skill(C),status(D),req(V,C,D).

person(peter,Y,Z):-skill(Y),status(Z),(Y=python;Y=sql),(Z=middle).
person(mary,Y,Z):-skill(Y),status(Z),(Y=excel;Y=sql;Y=english),(Z=student).
person(kira,Y,Z):-skill(Y),status(Z),(Y=python;Y=sql;Y=english),(Z=junior).

workman(N,V,C,D):-work(V,C,D),person(N,C,D).
```
% запросы:
```
?- workman(N,V,Y,Z). %и его вариации, можно искать подходящую вакансию по имени, статусу или скиллу
?- person(peter,Y,Z). %данные по человеку
?- work(V,C,D). %вакансии и их требования по скилам и статусу
```
