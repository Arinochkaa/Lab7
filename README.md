# Lab7
Лабораторная работа № 7
Тема: Работа с файловой системой.
Цель: Научиться сохранять данные в текстовый файл и считывать из
него.
Задание:
1. Разработали простое мобильное приложение для сохранения
данных из поля в тестовый файл, а также считывали информацию
из него;

Порядок выполнения:
1. Создали новый проект;
2. Добавили поле Plain Text, TextView, а также 2 кнопки –
«Сохранить в файл» и «Открыть из файла»;
3. Написали обработчик события для кнопки «Сохранить в файл»:
4. Написали обработчик события для кнопки «Открыть из файла»:
5.Установили разрешение на доступ в файле «AndroidManifest.xml»:
6. Назначили имя файла и установили путь для него:
7. Проверили работоспособность;

```Java
package com.example.myapplication;

import android.os.Environment;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.TextView;
import android.widget.Toast;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;

public class MainActivity extends AppCompatActivity {
    String fileName = "content.txt";
    File file = new
    File(Environment.getExternalStorageDirectory().getAbsolutePath(), fileName);

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }


    public void buttonSaveClick(View view) {
        try {
            TextView textBox = (TextView) findViewById(R.id.save_text);
            String text = textBox.getText().toString();

            FileOutputStream fos = new FileOutputStream(file);
            fos.write(text.getBytes());
            fos.close();
            Toast.makeText(this, "Текстовый файл успешно сохранён!",
                    Toast.LENGTH_SHORT).show();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
            Toast.makeText(this, "Файл не найден!",
                    Toast.LENGTH_SHORT).show();
        } catch (IOException e) {
            e.printStackTrace();
            Toast.makeText(this, "Ошибка сохранения файла!",
                    Toast.LENGTH_SHORT).show();
        }
    }

    public void buttonOpenClick(View view) {
        try {
            FileInputStream fin = new FileInputStream(file);
            byte[] bytes = new byte[fin.available()];
            fin.read(bytes);
            String text = new String(bytes);
            TextView textView = (TextView) findViewById(R.id.open_text);
            textView.setText(text);
            fin.close();
        } catch (IOException ex) {
            Toast.makeText(this, ex.getMessage(),
                    Toast.LENGTH_SHORT).show();
        }
    }
}
```
