# MobileNet-Digit-Recognition-for-DE0-CV
This project is a migration of a related project based on DE0-Nano
# Распознавание рукописных чисел при помощи ПЛИС
## Введение 
Данный проект является исследованием способа распознавания рукописных чисел при помощи ПЛИС, с последуещей миграцией проекта на плату, отличную от предложенной в базовой версии проекта. Этот проект использует исходный код из [данного репозитория](https://github.com/ZFTurbo/Verilog-Generator-of-Neural-Net-Digit-Detector-for-FPGA).
## Работа с MobileNet для DE0-Nano
Для работы с исходным репозиторием, обучения нейросети и последуещего синтеза проекта на плате необходимо провести изначальную подготовку системы. На практике сработала следующая комбинация версий библиотек и языков программирования:
* Tensorflow 1.5.0
* Keras 2.1.5
* Numpy 1.17.3
* OpenCV Python 4.1.1.26
* Python 3.6.1

После установки всех необходимых библиотек необходимо поочередно запустить файлы 
* r01_train_neural_net_and_prepare_initial_weights.py
* r02_rescale_weights_to_use_fixed_point_representation.py
* r03_find_optimal_bit_for_weights.py
* r04_verilog_generator_grayscale_file.py
* r05_verilog_generator_neural_net_structure.py

используя Python версии 3.6.1.

Данные файлы проводят обучение нейронной сети посредством Tensorflow, преобразуют полученные веса в представление машинное представление числа, и генерируют все необходимы файлы для синтеза проекта на языке SystemVerilog. Далее необходимо скомпилировать проект в среде Quartus и залить его на плату.

## Миграция проекта на плату DE0-CV
Для миграции проекта было необходимо провести работу с Pin Planner исходного проекта, вытащить оттуда названия пинов в проекте и их номера на плате. Затем по мануалам DE0-Nano были восстановлены их исходные названия и точное назначение. Затем при помощи мануала DE0-CV были найдены соответствующие по функционалу пины для внутреннего взаимодействия чипа и переферии. Затем были подобраны пины GPIO для взаимодействия с внешней переферией(камерой и экраном). После этого была составлена схема подключения внешней переферии. В таблице [DE0-Nano_DE0-CV_Pin_Migration](https://docs.google.com/spreadsheets/d/1A0XPAW9Wju027varuxUDcW01LeApagPy6rD0ONnkeG8/edit?usp=sharing) приведены данные действия.
### Подключение камеры и экрана к GPIO
Блок GPIO 0

![Alt text](//https://github.com/pavllan90/MobileNet-Digit-Recognition-for-DE0-CV/blob/master/images/Снимок%20экрана%202019-11-11%20в%2018.35.17.png "Блок GPIO_0")

Блок GPIO 1

![Alt text](//https://github.com/pavllan90/MobileNet-Digit-Recognition-for-DE0-CV/blob/master/images/Снимок%20экрана%202019-11-11%20в%2018.34.35.png "Блок GPIO_1")
