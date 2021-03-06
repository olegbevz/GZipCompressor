# GZipCompressor
Консольная утилита для сжатия и восстановления (декомпрессии) файлов, использующая метод GZip (алгоритм DEFLATE).

Инструкция по использованию:  
1. Сжатие файла: GZipCompressor.exe compress [имя файла] [имя архива]  
2. Восстановление файла: GZipCompressor.exe decompress [имя архива] [имя файла]  
3. Отмена операции: Ctrl+C  

Алгоритм сжатия файла:  
1. Исходный файл разбивается на блоки данных заданного размера (по умолчанию 10 мб).  
2. Для каждого блока создается поток. Максимальное количество потоков ограничивается указанным числом (по умолчанию 5).  
3. В отдельных потоках программа считывает блоки из исходного файла и сжимает их.  
4. В отдельных потоках сжатые блоки заносятся в очередь на запись в архив. Максимальное количество блоков в очереди на запись ограничивается указанным числом (по умолчанию 10).  
5. В отдельном потоке сжатые блоки последовательно извлекаются из очереди и записываются в файл архива.  

Алгоритм восстановления (декомпресии) файла:  
1. Выполняется последовательное считывание сжатых блоков данных из архива. Начало сжатого блока определяется с помощью стандартного заголовка формата GZIP (https://www.ietf.org/rfc/rfc1952.txt).  
2. Для каждого сжатого блока создается поток. Максимальное количество потоков ограничивается указанным числом (по умолчанию 5).  
3. В отдельных потоках программа считывает блоки из архива и распаковывает их. Для поддержки больших блоков данных блоки считываются и распаковываются по частям (подблокам). Размер части по умолчанию: 10 мб.  
4. В отдельных потоках распакованные блоки заносятся в очередь на запись в файл. Максимальное количество блоков в очереди на запись ограничивается указанным числом (по умолчанию 10).  
5. В отдельном потоке распакованные блоки последовательно извлекаются из очереди и записываются в файл.  
