cmake_minimum_required(VERSION 3.10)
project(RPNCalculator)

set(CMAKE_CXX_STANDARD 11)

# Включаем директории с исходными файлами
include_directories(include)

# Добавляем исполняемый файл основной программы
add_executable(rpn_calculator
    src/main.cpp
    src/rpn.cpp
)

# Устанавливаем свойства для более строгой компиляции
set_target_properties(rpn_calculator PROPERTIES
    CXX_STANDARD_REQUIRED YES
    CXX_EXTENSIONS NO
)

# КОНФИГУРАЦИЯ ТЕСТОВ
# Поиск GoogleTest
find_package(GTest REQUIRED)
include_directories(${GTEST_INCLUDE_DIRS})

# Добавляем тестовый исполняемый файл
add_executable(rpn_test
    tests/test_rpn.cpp
    src/rpn.cpp
)

# Линкуем тесты с gtest_main (вместо gtest)
target_link_libraries(rpn_test GTest::gtest_main pthread)

# Устанавливаем свойства для тестов
set_target_properties(rpn_test PROPERTIES
    CXX_STANDARD_REQUIRED YES
    CXX_EXTENSIONS NO
)

# Включаем систему тестирования CTest
enable_testing()

# Добавляем тест в CTest систему
add_test(NAME RPN_Calculator_Tests COMMAND rpn_test)