# Обработка видеофиксации транспорта MIET_Code

## Описание файлов
```MIET_Code_presentation.pptx``` - файл с презентацией решения

## Наше решение 
### Что успели сделать
Взяли готовую модель ```YOLOv8s```. К ней дописали алгоритм для детекции скорости: Если точка трекера объекта, прикреплённая к нижней части bbox пересекает первую  зону(поля 'zones' из json-файлов датасета), то bbox этого объекта становится bboxом 'интереса'. Затем, если трекер пересекает вторую зону, то мы начинаем рассчёт скорости с учётом расстояния в 20м. Если трекер не пересекает вторую зону, значит объект выехал из интересующей нас area в процессе движения, и скорость для такого объекта мы не считаем.

![Frame 1](https://github.com/Nikevich/Hak_MIET_Code/assets/111390447/056cb845-74eb-4934-ad30-0032bfd61a90)
В модель напрямую подаются сразу данные для inference и подготовки результата в виде ```.csv``` файла

### Что не успели
Из каждого видео в датасете мы берём 40 кадров. Затем эти кадры подаются в модель [Grounding DINO](https://github.com/IDEA-Research/GroundingDINO). Эта модель детектирует классы на изображении по текстовым промптам(эти промпты - это названия нужных нам классов). Затем мы подаём размеченные изображения для тренировки ```YOLOv8s```. После этого мы повторяем процедру для inference

![Frame 2](https://github.com/Nikevich/Hak_MIET_Code/assets/111390447/f050a325-7fd6-4958-9e00-367c9a29f92e)

### Что планируем делать в дальнейшем
Мы хотим аугментировать наши данные с помощью библиотеки [Albumentations](https://github.com/albumentations-team/albumentations). В качестве аугментаций планируем использовать наложение 'снега','дождя' и 'теней' на изображения. Это позовлить улучшить обобщаущую способность модели и её станет возможно использовать в том числе во время погодных условиях. 

![Grou (2)](https://github.com/Nikevich/Hak_MIET_Code/assets/111390447/83c8b8fe-3b7a-422e-a86e-191179fd5175)
