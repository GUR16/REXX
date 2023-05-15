# 
//**********************************************************************
//* ЗАДАНИЕ ПРЕДНАЗНАЧЕНО ДЛЯ ФОРМИРОВАНИЯ НАБОРА ДАННЫХ С КОМАНДАМИ   *
//* НА УДАЛЕНИЕ ПОЛЬЗОВАТЕЛЕЙ И ВСЕХ GENERAL RESOURCE К КОТОРЫМ ОНИ    *
//* ИМЕЮТ ДОСТУП                                                       *
//*                                                                    *
//* ------------------------------------------------------------------ *
//* ПРОГРАММА РАБОТАЕТ В НЕСКОЛЬКО ЭТАПОВ:                             *
//*                                                                    *
//*   1. ЗАПУСКАЕТСЯ ПРОГРАММА "UIRREXXT" ДЛЯ СБОРА ЗАБЛОКИРОВАННЫХ    *
//*      ПОЛЬЗОВАТЕЛЕЙ В СИСТЕМЕ ПО ЗАДАННЫМ ПАРАМЕТРАМ                *
//*                                                                    *
//*      OUTPUT = ВРЕМЕННЫЙ НАБОР ДАННЫХ С ЗАБЛОКИРОВАННЫМИ            *
//*               ПОЛЬЗОВАТЕЛЯМИ И ИНФОРМАЦИЕЙ ПО НИМ ИЗ RACF          *
//*      ПЕРЕДАЕТСЯ НА ВХОД В ПРОГРАММУ "DUAGREX2" И УДАЛЯЕТСЯ         *
//*                                                                    *
//*   2. ЗАПУСКАЕТСЯ ПРОГРАММА "DUAGREXX" ДЛЯ ФОРМИРОВАНИЯ ПОСТРОЧНОГО *
//*      СПИСКА АКТИВНЫХ КЛАССОВ, ПОЛЬЗОВАТЕЛЕЙ И                      *
//*      В ФОРМАТЕ: 1 СТОЛБЕЦ - ИМЯ АКТИВНОГО КЛАССА                   *
//*                 2 СТОЛБЕЦ - ПОЛЬЗОВАТЕЛЬ ИМЕЮЩИЙ ДОСТУП            *
//*                 3 СТОЛБЕЦ - ИДЕНТИФИКАТОР ДОСТУПА (READ,CONTROL..) *
//*                 4 СТОЛБЕЦ - ПРОФИЛЬ АКТИВНОГО КЛАССА               *
//*                                                                    *
//*      OUTPUT = ФОРМАТИРОВАННЫЙ ВРЕМЕННЫЙ НАБОР ДАННЫХ               *
//*      ПЕРЕДАЕТСЯ НА ВХОД В ПРОГРАММУ "SORT" И УДАЛЯЕТСЯ             *
//*                                                                    *
//*   3. ЗАПУСКАЕТСЯ ПРОГРАММА СОРТИРОВКИ СФОРМИРОВАННОГО Н.Д.         *
//*      (РЕЗУЛЬТАТ РАБОТЫ DUAGREXX)                                   *
//*                                                                    *
//*      ВХОДНОЙ НАБОР ДАННЫХ СОСТОИТ ИЗ СТРОК ТАКОГО ФОРМАТА:         *
//*        "ACTIVE CLASSES" "USERNAME" "ACCESS" "NAME"                 *
//*      ПРИМЕР: FACILITY ADMINS READ CBD.CPC.IPLARM                   *
//*                                                                    *
//*      ПРОГРАММА СОРТИРУЕТ ВРЕМЕННЫЙ Н.Д В ТАКОЙ ПОСЛЕДОВАТЕЛЬНОСТИ: *
//*         ВТОРОЙ СТОЛБЕЦ -> ПЕРВЫЙ СТОЛБЕЦ -> ЧЕТВЕРТЫЙ СТОЛБЕЦ      *
//*                                                                    *
//*      OUTPUT = ОТСОРТИРОВАННЫЙ НАБОР ДАННЫХ "DUAGR.SORT.OUT"        *
//*               ПО КРИТЕРИЯМ ОПИСАННЫМ ВЫШЕ                          *
//*                                                                    *
//*   4. ОТСЛЕЖИВАЕМ ЗАВЕРШЕНИЕ РАБОТЫ ПРОГРАММЫ СОРТИРОВКИ            *
//*      В СЛУЧАЕ УСПЕХА                                               *
//*      ЗАПУСКАЕТСЯ ПРОГРАММА "DUAGREX2" КОМПОНОВКИ НАБОРОВ ДАННЫХ С  *
//*      КОМАНДАМИ НА УДАЛЕНИЕ ЗАБЛОКИРОВАННЫХ ПОЛЬЗОВАТЕЛЕЙ ИЗ RACF И *
//*      GENERAL RESOURCE                                              *
//*                                                                    *
//*      OUTPUT =   1. НАБОР ДАННЫХ DUAGR.OUT1 С КОМАНДАМИ НА УДАЛЕНИЕ *
//*                    ЗАБЛОКИРОВАННЫХ ПОЛЬЗОВАТЕЛЕЙ ИЗ RACF           *
//*                 2. НАБОР ДАННЫХ DUAGR.OUT2 С КОМАНДАМИ НА УДАЛЕНИЕ *
//*                    ЗАБЛОКИРОВАННЫХ ПОЛЬЗОВАТЕЛЕЙ ИЗ                *
//*                    GENERAL RESOURCE                                *
//*                                                                    *
//*      НАБОР ДАННЫХ "DUAGR.SORT.OUT" УДАЛЯЕТСЯ                       *
//**********************************************************************
