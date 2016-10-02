# Адреса РФ (КЛАДР, ФИАС)

Проект создан для предоставления возможности удобного использования структурированной адресной информации в веб-системах без необходимости хранения и обеспечения актуализации данных адресов РФ. Все необходимые материалы находятся в свободном доступе.

Репозиторий содержит [структурированные данные](https://github.com/GitDataOrg/AddressRU/data/), сформированные на основе классификатора адресов Российской Федерации (КЛАДР), поддерживаемой Федеральной информационной адресной системой ([ФИАС](http://fias.nalog.ru/)), а также [программный модуль javascript](https://github.com/GitDataOrg/AddressRU/gitdata-address.js) для работы с данными.

Копия данных доступна на станице проекта GitData <http://address.gitdata.ru>, размещенной на [серверах Google](https://firebase.google.com).

## Описание
В папке `data` находятся файлы в формате json, расформированные по адресным объектам (их описание ниже). Каждый файл содержит все необходимые данные, относящиеся к объекту напрямую. На пример, файл [`77.json`](https://address.gitdata.ru/data/77.json) содержит все районы, города, населенные пункт и улицы Москвы (всего 209 Кб). Объекты разделены в соответствии с КЛАДР по уровням.

Таким образом, в процессе заполнения формы адреса при выборе пользователем значения элемента адреса достаточно подгрузить единственный файл данных, который содержать всю необходимую информацию для остальных элементов.

Следует заметить, что файлы содержат данные, напрямую касающиеся конкретного элемента, но ни как все всю иерархию подчиненных значений. Было бы неэффективно выкачивать массив данных, к примеру, даже для города. Поэтому детализированные данных запрашиваются по мере заполнения формы адреса. Одной из главных задача разработки является скорость предоставления данных для пользователя.

> Рабочие файлы данных доступны на [`https://address.gitdata.ru/data/`](https://address.gitdata.ru/data/)

> Список регионов находится в файле [`00.json`](https://address.gitdata.ru/data/00.json)

> Список используемых сокращений - в файле [`socrbase.json`](https://address.gitdata.ru/data/socrbase.json)

> В записях адресов используются числовые коды сокращений. Коды сокрашений указаны в `socrbase.json`


**Нагляднее на примере:**
В форме при обработке выбора пользователем в поле регион значения Чувашская республика (код 21), необходимо подгрузить файл [`21.json`](https://address.gitdata.ru/data/21.json) (1,01 Кб), в котором содержатся только 5 городов и 21 район республики (это так, потому что остальные города, населенные пункты и улицы относятся к напрямую подчиненным региону объектам). Далее при выборе из полученного списка города Новочебоксарск (код 21000024), загружается файл [`21000024.json`](https://address.gitdata.ru/data/21000024.json) (3,51 Кб), содержащий все улицы города (населенных пунктов в подчинении нет).
Итого для получения точного адреса, учитывая файл регионов [`00.json`](https://address.gitdata.ru/data/00.json) (3,13 Кб), было скачено 9,16 Кб (по расчету операционной системы Windows).

> В настоящий момент проект готовится к запуску, поэтому файлы и данные не оптимизированы. Позже этот объем будет существенно сокращен.

_К сведению самый большой размер 221 Кб имеет файл [`64000001.json`](https://address.gitdata.ru/data/64000001.json), относящийся к городу Саратов._ 

_**Общий объем файлов - 61,2 Мб**._


_Для сравнения размер 'минифицированного' файла `3.1.0/jquery.min.js` составляет 84,3 Кб, `1.11.2/jquery-ui.min.js` - 233 Кб, `15.0.1/react.min.js` - 142 Кб, `2.0.0-beta.17/angular2.min.js` - 621 Кб, стартовая страница поисковика Google - 390 Кб, Яндекс - 127 Кб (цифры со временем могут несущественно отличаться, важен порядок размера)._

## Формат КЛАДР
Классификационный код адресного объекта отражает иерархию его подчиненности и выделяет его среди объектов данного уровня, подчиненных одному и тому же старшему объекту. Классификационный код любого адресного объекта, начиная от регионов и улицами, представляется в следующем виде:
```
СС + РРР + ГГГ + ППП + УУУУ
```

Уровень | Код  | Количество знаков | Описание
--------|------|-------------------|--------------------------------------------
1       | СС   | 2                 | код субъекта Российской Федерации – региона
2       | РРР  | 3                 | код района
3       | ГГГ  | 3                 | код города
4       | ППП  | 3                 | код населенного пункта
5       | УУУУ | 4                 | код улицы

Города Москва (код 77) и Санкт-Петербург (код 78) выделены ФНС в отдельные региональные зоны.

С официальной документацией можно ознакомиться на [сайте ФИАС](http://fias.nalog.ru/Updates.aspx).

## Дата актуальности данных
29.09.2016

## Примечание
Федеральная информационная адресная система (ФИАС) - федеральная государственная информационная система, обеспечивающая формирование, ведение и использование государственного адресного реестра.

ФИАС начал функционировать на территории всей России с 1 ноября 2011 года в рамках реализации распоряжения Правительства Российской Федерации от 10.06.2011 № 1011-р.

1 июля 2014 года вступил в силу Федеральный закон от 28.12.2013 № 443-ФЗ «О федеральной информационной адресной системе и о внесении изменений в Федеральный закон «Об общих принципах организации местного самоуправления в Российской Федерации», который закрепил существование ФИАС и определил полномочия органов государственной власти и органов местного самоуправления в области отношений, возникающих в связи с ведением государственного адресного реестра, эксплуатацией федеральной информационной адресной системы, использованием содержащихся в государственном адресном реестре сведений об адресах.

Ранее КЛАДР был создан для распределения территорий между налоговыми инспекциями и автоматизированной рассылки корреспонденции и служил внутренним ведомственным классификатором ФНС России.

## Отказ от ответственности
В репозиторие опубликована копия данных адресного классификатора, сформатированная в структурированном текстом представлении в формате json. Содержание данных правке не подвергались. Ответственность за достоверность и полноту информации адресного классификатора, согласно [Постановлению Правительства Российской Федерации от 29.04.2014 № 384](http://government.ru/docs/all/91170/), несет ФНС России.

## Авторские права
База данных, содержащаяся в репозиторие, предоставляется [Федеральной налоговой службой России](http://www.nalog.ru) и находится в свободном публичном доступе на специализированном портале ФИАС <http://fias.nalog.ru>.

Права на публикуемый программный модуль javascript принадлежат [группе разработки GitData](http://www.gitdata.net). Программный модуль распространяется в открытом доступе без ограничений на использование. Полный текст лицензии опубликован ниже.

## Лицензия
Данная лицензия разрешает лицам, получившим копию данного программного обеспечения и сопутствующей документации (в дальнейшем именуемыми «Программное Обеспечение»), безвозмездно использовать Программное Обеспечение без ограничений, включая неограниченное право на использование, копирование, изменение, слияние, публикацию, распространение, сублицензирование и/или продажу копий Программного Обеспечения, а также лицам, которым предоставляется данное Программное Обеспечение, при соблюдении следующих условий:
Указанное выше уведомление об авторском праве и данные условия должны быть включены во все копии или значимые части данного Программного Обеспечения.

ДАННОЕ ПРОГРАММНОЕ ОБЕСПЕЧЕНИЕ ПРЕДОСТАВЛЯЕТСЯ «КАК ЕСТЬ», БЕЗ КАКИХ-ЛИБО ГАРАНТИЙ, ЯВНО ВЫРАЖЕННЫХ ИЛИ ПОДРАЗУМЕВАЕМЫХ, ВКЛЮЧАЯ ГАРАНТИИ ТОВАРНОЙ ПРИГОДНОСТИ, СООТВЕТСТВИЯ ПО ЕГО КОНКРЕТНОМУ НАЗНАЧЕНИЮ И ОТСУТСТВИЯ НАРУШЕНИЙ, НО НЕ ОГРАНИЧИВАЯСЬ ИМИ. НИ В КАКОМ СЛУЧАЕ АВТОРЫ ИЛИ ПРАВООБЛАДАТЕЛИ НЕ НЕСУТ ОТВЕТСТВЕННОСТИ ПО КАКИМ-ЛИБО ИСКАМ, ЗА УЩЕРБ ИЛИ ПО ИНЫМ ТРЕБОВАНИЯМ, В ТОМ ЧИСЛЕ, ПРИ ДЕЙСТВИИ КОНТРАКТА, ДЕЛИКТЕ ИЛИ ИНОЙ СИТУАЦИИ, ВОЗНИКШИМ ИЗ-ЗА ИСПОЛЬЗОВАНИЯ ПРОГРАММНОГО ОБЕСПЕЧЕНИЯ ИЛИ ИНЫХ ДЕЙСТВИЙ С ПРОГРАММНЫМ ОБЕСПЕЧЕНИЕМ.

Указанное выше уведомление об авторском праве и данные условия должны быть включены во все копии или значимые части данного Программного Обеспечения.
_(Текст лицензии идентичен лицензии MIT на английском языке)_

## Дорожная карта проекта

Работы много, планов множество. Будем благодарны для вашу любую помощь или поддержку.

- Основной целью является скорость предоставления данных на форму. Поэтому приоритетны вопросы сжатия, компоновки, форматирования данных для уменьшения объемов. Для сокращения времени загрузки файлов рассматриваются варианты использования CDN и геопозиционированные скоростные ресурсы облачных хранилищ.

- Нацеленность на удобство пользования тоже крайне важна при разработке. Проект будет жить, пока им будут пользоваться. Понимание этого достаточно для оценки решений с точки зрения использования.

- Для уменьшения объемом файлов рассматривается вариант создание базы без использования почтового индекса.

- Рассматривается вариант разделения кодоы объектов на отдельные составные числовые части.

- Для удобства использования будет прорабатываться вопрос интеграции адресного классификатора с geoIP. Это даст возможность заранее подгружать необходимые (с большой долей вероятности) для пользователя данные.

- Изучаются технологии сжатия текстовых файлов и возможности форматирования данных. К примеру, внедрение словарей.


**В процессе разработки крайне необходимы отзывы и напутствия пользователей, поэтому, пожалуйста, если Вас заинтересовал проект как разработчика или как пользователя, свяжитесь с нами. Мы будем благодарны любым отзывам и предложениям здесь или по электронной почте <support@gitdata.net>.



## Ссылки
- [Официальный сайт ФИАС](http://fias.nalog.ru)
- [Прямая ссылка на актуальную базу КЛАДР](http://fias.nalog.ru/Public/Downloads/Actual/base.arj)
- [Описание формата JSON](https://tools.ietf.org/html/rfc4627)
- Сайт группы разработки <http://www.gitdata.net>
- [Станица проекта на GitData](http://address.gitdata.ru)
- [Проект на Google Firebase](https://gitaddress.firebaseapp.com)
