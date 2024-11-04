# Практическая работа 1

CREATE TABLE `books` (
  `idbooks` INT NOT NULL AUTO_INCREMENT,
  `title` VARCHAR(45) NOT NULL,
  `author` VARCHAR(45) NOT NULL,
  `year` INT NOT NULL,
  `price` INT UNSIGNED NOT NULL,
  PRIMARY KEY (`idbooks`));



INSERT INTO `books` (`title`, `author`, `year`, `price`) VALUES ('Убить пересмешника', 'Харпер Ли  ', '1960', '300');

INSERT INTO `books` (`title`, `author`, `year`, `price`) VALUES ('1984', 'Джордж Оруэлл  ', '1949 ', '250');

INSERT INTO `books` (`title`, `author`, `year`, `price`) VALUES ('Великий Гэтсби ', 'Ф. Скотт Фицджеральд ', '1925', '200');

INSERT INTO `books` (`title`, `author`, `year`, `price`) VALUES ('Над пропастью во ржи', 'Дж. Д. Сэлинджер ', '1951', '280');
INSERT INTO `books` (`title`, `author`, `year`, `price`) VALUES ('Моби ДИк', 'Герман Мелвилл', '1851', '400');
INSERT INTO `books` (`title`, `author`, `year`, `price`) VALUES ('Скотный двор', 'Джордж Оруэлл', '1945', '220');
INSERT INTO `books` (`title`, `author`, `year`, `price`) VALUES ('Почти на Каталонии ', 'Джордж Оруэлл', '1938 ', '180');



# Итоговая контрольная 

`````
-- Создание функции для форматирования секунд
DELIMITER //

CREATE FUNCTION format_seconds(total_seconds INT)
RETURNS VARCHAR(100)
DETERMINISTIC
BEGIN
    DECLARE days INT;
    DECLARE hours INT;
    DECLARE minutes INT;
    DECLARE seconds INT;

    SET days = total_seconds DIV 86400;
    SET hours = (total_seconds % 86400) DIV 3600;
    SET minutes = (total_seconds % 3600) DIV 60;
    SET seconds = total_seconds % 60;

    RETURN CONCAT(days, ' days ', hours, ' hours ', minutes, ' minutes ', seconds, ' seconds');
END //

DELIMITER ;

-- Пример использования функции
SELECT format_seconds(123456) AS formatted_time;

-- Вывод четных чисел от 1 до 10
SELECT num
FROM (
    SELECT 1 AS num UNION ALL
    SELECT 2 UNION ALL
    SELECT 3 UNION ALL
    SELECT 4 UNION ALL
    SELECT 5 UNION ALL
    SELECT 6 UNION ALL
    SELECT 7 UNION ALL
    SELECT 8 UNION ALL
    SELECT 9 UNION ALL
    SELECT 10
) AS numbers
WHERE num % 2 = 0;
`````

