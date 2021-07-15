cmake_minimum_required(VERSION 3.2) #устанавливаем версию СMake
set(CMAKE_CXX_STANDARD 11) #определяем используемый стандарт
set(CMAKE_CXX_STANDARD_REQUIRED ON) #обеспечиваем поддержку данного стандарта
project(bank) #даём проекту название 
SET(COVERAGE OFF CACHE BOOL "Coverage") #создаём кэшированную переменную COVERAGE типа BOOL и отключаем её (OFF);"Coverage" - короткое описание переменной COVERAGE
enable_testing() #Включите тестирование для текущего каталога и ниже.
add_subdirectory(gtest) #Добавляет подкаталог в сборку. source_dir указывает каталог, в котором находится источник CMakeLists.txt и файлы кода находятся. 
include_directories(${gtest_SOURCE_DIR}/include ${gtest_SOURCE_DIR}) #Добавьте указанные каталоги в те, которые компилятор использует для поиска включенных файлов.
add_library(lib1 Account.h Account.cpp) #из файлов Account.h Account.cpp создаётся библиотека lib1 
add_library(lib2 Transaction.h Transaction.cpp) #из файлов Transaction.h Transaction.cpp создаётся библиотека lib2
add_executable(runUnitTests test.cpp) #создаётся исполняемый файл runUnitTests
target_compile_options(runUnitTests PRIVATE --coverage) #для исполняемого файла runUnitTests устанавливаем следующие параметры компиляции: 
#PRIVATE - необходим для указания области действия аргумента --coverage
target_link_libraries(runUnitTests PRIVATE --coverage gtest gtest_main)#указываются библиотеки или флаги, которые будут использоваться при связывании данного целевого объекта и/или его зависимостей. 
add_test( runUnitTests runUnitTests ) #добавляется тест в проект, который будет выполняться ctest()-это программа тестового драйвера CMake.
