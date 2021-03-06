Лабораторная работа №1 по дисциплине "Инжинерная и компьютерная графика"

Создание окна

```C++
glutInit(&argc, argv);
//Здесь мы инициализируем GLUT
glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGBA);
//Так настраиваются некоторые опции GLUT. GLUT_DOUBLE включает двойную буферизацию
glutInitWindowSize(1024, 768);
//Задаем размер окна
glutInitWindowPosition(100, 100);
//Задаем позицию окна
glutCreateWindow("Tutorial 01");
//Задаем имя окна
glutDisplayFunc(RenderSceneCB);
//Отрисовываем 1 кадр
glClearColor(0.0f, 0.0f, 0.0f, 0.0f);
//Устанавливаем цвет, который будет использован во время очистки буфера кадра. Цвет имеет 4 канала (красный, зелёный, синий, альфа-канал) и принимает значения от 0.0 и до 1.0
glutMainLoop();
//Этот вызов передаёт контроль GLUT'у, который теперь начнёт свой собственный цикл
```

Функция отрисовки

```C++
static void RenderSceneCB()
{
    glClear(GL_COLOR_BUFFER_BIT);
    //Очистка буфера кадра
    glutSwapBuffers();
    //Функция просит GLUT поменять фоновый буфер и буфер кадра местами
}
```

Рисование точки

```C++
GLuint VBO; //указатель на буфер вершин
```
В main() добавляем:

```C++
glm::vec3 Vertices[1];
//Создание вектора вершины
Vertices[0] = glm::vec3(0.0f, 0.0f, 0.0f);
// создаем вектор с координатами x, y, z 
glGenBuffers(1, &VBO);
//генерация объектов переменных типов
glBindBuffer(GL_ARRAY_BUFFER, VBO);
//буфер будет хранить массив вершин
glBufferData(GL_ARRAY_BUFFER, sizeof(Vertices), Vertices, GL_STATIC_DRAW);
//наполняем объект данными
```

В RenderSceneCB() добавляем:

```C++
glEnableVertexAttribArray(0);
//координаты вершин, используемые в буфере, рассматриваются как атрибут вершины с индексом 0
glBindBuffer(GL_ARRAY_BUFFER, VBO);
//обратно привязываем наш буфер, приготавливая его для отрисовки
glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 0, 0);
//говорим конвейеру как воспринимать данные внутри буфера
glDrawArrays(GL_POINTS, 0, 1);
//вызвали функцию для отрисовки
glDisableVertexAttribArray(0);
//отключаем каждый атрибут вершины
```
