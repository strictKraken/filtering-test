# Описисание выполнения тестового задания

Для фильтрации использовал метод filter.

Проверка будет простой

Значения которые пользователь вводит [inputStart inputEnd] 
левую границу проверяем с правой границей элементов из словаря с данными
правую границу проверяем с левой границей элементов из словаря с данными

1) courses[prices][1] < inputStart ? return false

2) courses[prices][0] > inputEnd ? return false

3) Все остальные значения true

Этого достаточно чтобы отфильтроватьнужные диапазоны значений. Остальное это обработка значений null, я не знаю как точно обрабатывать в данном случае null решить определить их так, левая граница null ~ 0 правая граница null ~ +бесконечность.

 

И необходимо обработать значения пустой строки. Думаю можно было реализовать это более красиво, но получилось пока так.

### Код фильтрации

```jsx
const startFilter = () => {
           coursesTmp.value = [...props.courses].filter(item => {
		//Если ввели начальное значение больше конечного значения а так же проверка на null и пустую строчку
                if(startNumber.value > endNumber.value && (startNumber.value !== null && startNumber.value !== '') && (endNumber.value !== null && endNumber.value !== '')) return false;
		//Если оба значения элемента словаря он будет выводится всегда
                if(item[keyDict][0] === null && item[keyDict][1] === null) return true;
		//Проверка 1 правой границы элемента словаря
                if(startNumber.value > item[keyDict][1] && item[keyDict][1] !== null ) {
                    //Если вводимые значения пустые
										if(startNumber.value === null || startNumber.value === '') return true;
                    return false;
                }
		//Проверка 2 левой границы словаря
                if(endNumber.value < item[keyDict][0] && item[keyDict][0] !== null) {
                    if(endNumber.value === null || endNumber.value === '') return true;
                    return false;
                }
                //Если вводимые значения пустые
                if(startNumber.value === null || startNumber.value === '') return true;
                return true;
            })
        }

```

Пришлось перенести код на разные строчки чтобы поместились на лист.

### Код сортировки

```jsx
function sortCurses() {
            let tmp = aTure;
            aTure = bTrue;
            bTrue = tmp;
            coursesTmp.value =  coursesTmp.value.sort((a,b) => {
                return a[keyDict][0] < b[keyDict][0] ? aTure : bTrue;
            })
        }
```

Полный код находится в /src/components/CoursesPage.vue [https://github.com/strictKraken/filtering-test/tree/main/src/components](https://github.com/strictKraken/filtering-test/tree/main/src/components)

Рабочий тест находится по адресу [https://strictkraken.github.io/filtering-test/](https://strictkraken.github.io/filtering-test/)
