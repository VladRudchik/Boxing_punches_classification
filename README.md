# Boxing_punches_classification
Boxing punches сlassification during a training fight using data science. Also, the resulting algorithm can be used to classify individual strokes.
## Contents

- [Formulation of the problem](#formulation-of-the-problem)
- [Contents of the repository](#contents-of-the-repository)
- [About the dataset](#about-the-dataset)

## Formulation of the problem
### Task:
Create a system that will highlight and classify the boxer's punches during training (training combat and individual punches).

For this purpose it is necessary to:

1) Come up with a system with which you will collect data
2) Collect dataset
3) Analyze the data obtained
4) Complete the data processing
5) Create a machine learning model that will highlight and classify punches
6) Test and analyze the results

You can see the solution to all these tasks in my presentation (Rudchyk_Boxing_Punch_Classif_ENG). Later in the README we will talk about filling the repository (Contents of jupyter notebook and сollected dataset).
## Contents of the repository
Files:
- boxing_punches_classification_final.ipynb, This is a ready-made notebook that takes a recording file, then filters the data, looks for punches in the recording and classifies them.
- boxing_punches_classification_markup.ipynb, The file that contains dataset markup indexes.
- Rudchyk_Boxing_Punch_Classif_ENG.pptx, A presentation in which all stages of solving the problem are shown in detail.
- Rudchyk_Boxing_Punch_Classif_UA.pptx, Презентація, що зазначена вище, але на українській мові, можливо комусь буде набагато зручніше). Обережно, там немає декількох правок які були внесені в Англ варіант, тому краще орієнтуватись на нього.
- boxing_punches_classification_workbook.ipynb, This is my workbook, which records the process of data analysis, selection of filters, search for features for models, selection of models and arguments for their use. There are also graphs I looked at while working and the main thoughts I had. Unfortunately, since this is a workbook, it is not very cleanly designed(. P.S. It's not very interesting and informative, but it might help if you want to use the dataset I've collected.

Folders:
- data, The collected dataset is divided into 3 folders, test and training data for the punches classification model, and training fight records for the punches detection model.
- model, Models for classification and detection have already been trained. There are several punches classification models,CatBoost worked best on my test data.

## About the dataset
### Збір даних
У моєму випадку збір даних виконувався телефоном прив'язаним до руку в місці, де повинен бути браслет (пробував тримати телефон в долоні екраном в руку, все продовжувало працювати).
Дані записувались за допомогою додатку Accelerometer Meter (ви його можете знайти в Google Play) на налаштуваннях (в розділі Graph) позначених на малюнку.

<img src="app_settings.jpg" width="350" height="300" />

Тобто модель використовує значення датчика в 	$m/s^{2}$ та при частоті 200 Гц.

### Train data
У зборі тренувального дата сета брали участь 4 молоді та здорові людини різних спортивних категорій, 10 + 9 + 8 + 5 в цілому 33 записи. 
По технічній частині збору даних описано вище.
Тренувальний запис мав такий формат:
1. 5 секунд спокою
2. 15 секунд махів руками
3. 10 сек відпочинку
4. 15 сек присідань
5. 10 сек відпочинку
6. 15 сек ударів руками
7. 5 сек спокою

У половині файлів під час спокою та відпочинку потрібно було тримати руки майже нерухомо, у половині можна було спокійно рухатись та виконувати інші дії (почесати спину та тд).
### Test data
У нас є 8 спеціально відзнятих файли для тесту (те що модель ні одного разу на них не промахнулась, це просто співпало), щоб перевірити всі можливі варіанти звіту та роботу алгоритму.
1. test1_standard - формат дій як і в трейні, виконаний людиною, дані якої є в трейні. (15 сек махів (в майбут. 15 м), 15 сек присідань (15 п), 15 сек ударів (15 у)).
2. test2_standard_other - формат дій як і в трейні, виконаний людиною, даних якої не має трейні. (15 м, 15 п, 15 у).
3. test3_stress - великий набір вправ у хаотичному порядку ранодомного часу. (10п, 20у, 15м, 10м, 8м, 10у, 12п, 10у, 10м), людини не має в трейні.
4. test4_not_full_squatting - не виконані всі присідання (15м, 15у, 5п), можна побачити, як алгоритм робить помилки, але основну задачу все таки виконує.
5. test5_only_hits - присутні тільки удари в повному обсязі (15у).
6. test6_not_squatting - повні удари, не всі махи, немає присідань (15у, 5м).
7. test7_only_not_full_rotation - тільки не повні махи (10м).
8. test8_error_file - файл з пошкодженою частою та середнім прискоренням, для перевірки частини пошуку помилок, (7м, 7у).

P.S. Відхилення часу дій в звітах від зазначених здебільшого помилка людини, яка виконувала дію невірний час, а не помилка алгоритму.
