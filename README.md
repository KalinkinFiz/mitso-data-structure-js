# Общее описание задачи

Ваша задача — разобраться с несколькими структурами данных, чтобы решить подзадачи. Описания подзадач, а также инструкции по запуску тестов и отправке решений находятся ниже.

---

### **Бинарное дерево поиска**

![Binary search tree](https://www.tutorialspoint.com/data_structures_algorithms/images/binary_search_tree.jpg)  
**Бинарное дерево** — это иерархическая **структура данных**, в которой каждый **узел** имеет **значение** (оно же является в данном случае и ключом) и **ссылки** на **левого** и **правого** **потомка**. **Узел**, находящийся на самом верхнем уровне (не являющийся чьим либо потомком) называется **корнем**. **Узлы**, не имеющие потомков, называются **листьями**.

**Бинарное дерево поиска** — это **бинарное дерево**, обладающее дополнительными свойствами: значение **левого** потомка **меньше** значения родителя, а значение **правого** потомка **больше** значения родителя для каждого **узла** дерева. То есть, данные в бинарном дереве поиска хранятся в отсортированном виде. При каждой операции **вставки** нового или **удаления** существующего узла отсортированный порядок дерева сохраняется. При **поиске** элемента сравнивается искомое значение с корнем. Если искомое **больше** корня, то поиск продолжается в **правом** потомке корня, если **меньше**, то в **левом**, если **равно**, то значение **найдено** и поиск прекращается.

Ваша задача — реализовать класс `BinarySearchTree`.
Каждый экземпляр `BinarySearchTree` должен обладать следующими методами:

- `root` — возвращает **корневой узел** дерева
- `add(data)` — добавляет **узел** с `data` к дереву
- `has(data)` — возвращает `true`, если **узел** с `data` имеется в дереве и `false`, если нет
- `find(data)` — возвращает **узел** с `data`, если **узел** с `data` имеется в дереве и `null`, если нет
- `remove(data)` — удаляет **узел** с `data` из дерева, если **узел** с `data` имеется в дереве
- `min` — возвращает **минимальное** **значение**, хранящееся в дереве (или `null`, если у дерева нет **узлов**)
- `max` — возвращает **максимальное** **значение**, хранящееся в дереве (или `null`, если у дерева нет **узлов**)

Например:

`const tree = new BinarySearchTree();`

`tree.add(1);`

`tree.add(2);`

`tree.add(3);`

`tree.add(4);`

`tree.add(5);`

`tree.root().data` => `1;`

`tree.min()` => `1`

`tree.max()` => `5`

`tree.remove(5);`

`tree.has(5)` => `false`

`tree.max()` => `4`

Напишите свой код в `src/binary-search-tree.js`.

---

### **Удалить из списка**

Дан **односвязный связный список** целых чисел (`l`) и целое число (`k`), удалите все элементы из списка `l`, содержащие значение `k`.

Например, для `l` = `[3, 1, 2, 3, 4, 5]` и `k` = `3`,
результат будет `[1, 2, 4, 5]`

Узлы односвязного связного списка определяются интерфейсом:

```js
function ListNode(x) {
  this.value = x;
  this.next = null;
}
```

Напишите свой код в `src/remove-from-list.js`.

---

### **Стек**

Реализуйте **стек** с заданным интерфейсом на основе **массива**.

Например:

```js
const stack = new Stack();

stack.push(1); // добавляет элемент в стек
stack.peek(); // возвращает верхний элемент, но не удаляет его, возвращает 1
stack.pop(); // возвращает верхний элемент и удаляет его, возвращает 1
stack.pop(); // undefined
```

Напишите свой код в `src/stack.js`.

---

### **Очередь**

Реализуйте **очередь** с заданным интерфейсом на основе **связного списка** (используйте `ListNode`, расположенный в папке `extensions`).
Каждый экземпляр очереди должен иметь 3 метода:
_ `enqueue(value)` — помещает `value` в конец **очереди**
_ `deque` — извлекает значение с начала **очереди** и удаляет его \* `getUnderlyingList` - возвращает **связный список**, лежащий в основе данной **очереди**

Например:

```js
const queue = new Queue();

queue.enqueue(1); // добавляет элемент в очередь
queue.enqueue(3); // добавляет элемент в очередь
queue.dequeue(); // возвращает элемент из начала очереди и удаляет его, возвращает 1
queue.getUnderlyingList(); // возвращает { value: 3, next: null }
```

Напишите свой код в `src/queue.js`.

---

### **Фильтр Блума**

**Фильтр Блума** - это пространственно-эффективная вероятностная структура данных, созданная для проверки наличия элемента
в множестве. Он спроектирован невероятно быстрым при минимальном использовании памяти ценой потенциальных ложных срабатываний.
Существует возможность получить ложноположительное срабатывание (элемента в множестве нет, но структура данных сообщает,
что он есть), но не ложноотрицательное. Другими словами, очередь возвращает или "возможно в наборе", или "определённо не
в наборе". Фильтр Блума может использовать любой объём памяти, однако чем он больше, тем меньше вероятность ложного
срабатывания.

Блум предложил эту технику для применения в областях, где количество исходных данных потребовало бы непрактично много
памяти, в случае применения условно безошибочных техник хеширования.

### Описание алгоритма

Пустой фильтр Блума представлен битовым массивом из `m` битов, все биты которого обнулены. Должно быть определено `k`
независимых хеш-функций, отображающих каждый элемент множества в одну из `m` позиций в массиве, генерируя единообразное
случайное распределение. Обычно `k` задана константой, которая много меньше `m` и пропорциональна
количеству добавляемых элементов; точный выбор `k` и постоянной пропорциональности `m` определяются уровнем ложных
срабатываний фильтра.

Вот пример Блум фильтра, представляющего набор `{x, y, z}`. Цветные стрелки показывают позиции в битовом массиве,
которым привязан каждый элемент набора. Элемент `w` не в наборе `{x, y, z}`, потому что он привязан к позиции в битовом
массиве, равной `0`. Для этой формы , `m = 18`, а `k = 3`.

Фильтр Блума представляет собой битовый массив из `m` бит. Изначально, когда структура данных хранит пустое множество, все
`m` бит обнулены. Пользователь должен определить `k` независимых хеш-функций `h1`, …, `hk`,
отображающих каждый элемент в одну из `m` позиций битового массива достаточно равномерным образом.

Для добавления элемента e необходимо записать единицы на каждую из позиций `h1(e)`, …, `hk(e)`
битового массива.

Для проверки принадлежности элемента `e` к множеству хранимых элементов, необходимо проверить состояние битов
`h1(e)`, …, `hk(e)`. Если хотя бы один из них равен нулю, элемент не может принадлежать множеству
(иначе бы при его добавлении все эти биты были установлены). Если все они равны единице, то структура данных сообщает,
что `е` принадлежит множеству. При этом может возникнуть две ситуации: либо элемент действительно принадлежит множеству,
либо все эти биты оказались установлены по случайности при добавлении других элементов, что и является источником ложных
срабатываний в этой структуре данных.

![Фильтр Блума](https://upload.wikimedia.org/wikipedia/commons/a/ac/Bloom_filter.svg)

### Применения

Фильтр Блума может быть использован для блогов. Если цель состоит в том, чтобы показать читателям только те статьи,
которые они ещё не видели, фильтр блума идеален. Он может содержать хешированные значения, соответствующие статье. После
того, как пользователь прочитал несколько статей, они могут быть помещены в фильтр. В следующий раз, когда пользователь
посетит сайт, эти статьи могут быть убраны из результатов с помощью фильтра.

Некоторые статьи неизбежно будут отфильтрованы по ошибке, но цена приемлема. То, что пользователь не увидит несколько
статей в полне приемлемо, принимая во внимание тот факт, что ему всегда показываются другие новые статьи при каждом
новом посещении.

### Ссылки

- [Wikipedia](https://ru.wikipedia.org/wiki/%D0%A4%D0%B8%D0%BB%D1%8C%D1%82%D1%80_%D0%91%D0%BB%D1%83%D0%BC%D0%B0)
- [Фильтр Блума на Хабре](https://habr.com/ru/post/112069/)

Напишите свой код в `src/bloom-filter.js`.

---

## Предварительные шаги

1. Установите [Node.js](https://nodejs.org/en/download/)
2. Сделайте **fork** этого репозитория: https://github.com/KalinkinFiz/mitso-data-structure-js
3. Склонируйте себе этот репозиторий: `git clone https://github.com/<%your_github_username%>/mitso-data-structure-js/`
4. Перейдите в папку **mitso-data-structure-js**: `cd mitso-data-structure-js`
5. Вбейте в командную строку [`npm install`](https://docs.npmjs.com/cli/install) для установки зависимостей.
6. Прочтите описание задачи в `README.md`.
7. Напишите свой код в src/\*.js

   Удалите строку с генерацией ошибки из тела функции:

   ```js
   throw new NotImplementedError("Not implemented");
   ```

   Реализуйте функцию любым способом и проверьте свое решение, запустив тесты.

8. Выполните `npm run test` в командой строке.
9. Вы увидите число ожидающих (pending), проходящих и падающих тестов. 100% проходящие тесты сооветствуют максимальному баллу за задание.
10. **Если все в порядке и задача решена, то необходимо:**
    - добавить содержимое измененного файла в index: `git add .` (все измененные файлы попадут в **index**) или `git add ./src/<название файда>.js`
    - записать изменения в локальный репозиторий: `git commit -m "текст коммита"`, например `git commit -m "feat: binarySearchTree completed"`
    - выгрузить новые коммиты из локальной ветки на удаленный репозиторий: `git push origin main`

### !!! ВАЖНО !!!

- Изменение тестов приравнивается к 0 баллов!
- Коммит === решение ОДНОЙ задачи.
