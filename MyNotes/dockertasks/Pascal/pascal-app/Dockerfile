# Используем готовый образ с Free Pascal
FROM primeimages/freepascal:3.2.2
WORKDIR /app
# Копируем исходный код
COPY hello.pas .
# Компилируем
RUN fpc hello.pas
# Запускаем
CMD ["./hello"]