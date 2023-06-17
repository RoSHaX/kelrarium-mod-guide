<h1 align="center">Кельрариум - Гайд по созданию модов.</h1>

# Предисловия

Привет всем! Меня зовут [Роман Шавинцев](https://vk.com/rosha586). Я являюсь автором гайда и кодером проекта "Кельрариум. Медовый погребок".

Конечно, данная новелла не была бы осуществлена без усердия всей команды разработчиков:

Основатель и сценарист данной визуальной новеллы - [Максим Печень](https://vk.com/id369782827), который вложил в проект душу.

Композиторы, [Artem Zebrev](https://vk.com/az_giametal) и [Yarrist](https://vk.com/yarrist_music), которые наполнили новеллу звуковым оформлением;.

Художники, [Педучилище Злобное](https://vk.com/id674208733), [D_SMILE](https://vk.com/d_smile_directory) и [BeTry](https://vk.com/betryy), которые создали красочные арты и спрайты.

Актуальную информацию по разработке проекта можно узнать в [нашей группе во ВКонтакте](https://vk.com/kelrarioom).

# Написание кода
Для начала нужно создать файл с расширением `.rpy.` Затем открыть его в текстовом редакторе и следовать инструкциям в руководстве.

Лично я предпочитаю использовать редактор кода Sublime Text 3, так как он удобен и мне уже знаком.

______________________________________________________________________________________

Для того, чтобы игра распознала файл как мод, необходимо написать следующее:
```Ren'py
init:
    $ cellars["my_mod"] = "Мой мод"
```
Давайте рассмотрим более подробно:

- *my_mod* - это название начального лейбла мода. При запуске мода этот лейбл является первым в списке на выполнение. Название должно быть уникальным, иначе возможны конфликты с другими модами, которые могут иметь лейблы с таким же названием. Используйте только латиницу!

- *Мой мод* - это название мода, которое будет отображаться в списке модов. Допускается использование кириллицы.

Теперь для того, чтобы игра могла определить, где начинается мод, необходимо добавить начальный лейбл:
```Ren'py
init:
    $ cellars["my_mod"] = "Мой мод"

label my_mod:
    "Текст(Реплика)"
```

# Написание сценария.
Далее, в метке my_mod можно начинать писать сценарий. Давайте разберёмся по порядку:

# Метки
Использование меток значительно облегчит процесс создания мода.
напомню, что имена меток должны быть уникальными, чтобы избежать конфликтов. Самым лучшим вариантом является назвать метку так же, как и мод, например my_mod_2.
```Ren'py
label my_mod_1:
    "..."
label my_mod_2:
    "..."
```
# Переходы между лейблами

Есть два вида переходов:

Прыжок (jump)

```Ren'py
label my_mod_1:
    "..."
    jump my_mod_2 # Прыжок на метку my_mod_2

label my_mod_2:
    "..."
```
В данном случае команды, написанные после "прыжка", будут проигнорированы игрой. Например, фраза "Ты меня видишь?" из примера ниже не будет выведена на экран игрока. Любые команды, написанные *после* "прыжка", также не будут выполнены.
```Ren'py
label my_mod_1:
    "..."
    jump my_mod_2
    "Ты меня видишь?"

label my_mod_2:
    "..."
```

# Вызов (call)
В этом случае фраза из примера выше будет выведена на экран после завершения действий из метки my_mod_2.
```Ren'py
label my_mod_1:
    "..."
    call my_mod_2 # Вызов второго лейбла
    "Ты меня видишь?" # После того, как нас выбросит из лейбла my_mod_2 командой return, появится данная фраза.
    
label my_mod_2:
    "..."
```
Завершить блок можно командой return. После нее мод будет закончен и на экране появится главное меню игры.

# Реплики
Реплика, или текст от имени персонажей, имеет следующий общий вид: <ID персонажа> "<Реплика>", где

- `ID персонажа` - название переменной, которой он был объявлен.
- `Реплика` - текст, который будет произнесен персонажем.

Список персонажей и их переменные представлены в таблице ниже:

| переменная | персонаж | 
| ---------- | ------   | 
| `kas`      | Казимир  | 
| `wolfg`    | Волчица  |
| `scar`     | Скарлетт |
| `milki`    | Молочница|
| `maf`      | Мафую    |
| `ayla`     | Айла     |
| `girl`     | Девочка  |
| `noth`     | ...      |

# Изображения
Чтобы вывести фон или иллюстрацию, можно использовать следующие команды:

- scene <название фона/иллюстрации>

- show <название иллюстрации>

*В чём разница?* - Разница между командами scene и show заключается в следующем: 

Команда scene <название фона/иллюстрации> очищает все слои и показывает только указанное изображение в качестве заднего фона.

Команда show <название иллюстрации> показывает указанное изображение поверх других изображений, уже имеющихся на экране, без очистки слоев.

Фоны из игры представлены в таблице ниже:


| Код             | Предпросмотр   |
| ----------------| ---------------------------------------------------------------------------------------------------------------------- |
| `scene Misly`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/c2c6c7e0-5327-40e2-9622-929490df7ee3" width="300">|
| `scene Port_day`  | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/2cd3e3a7-c8af-4cf6-82a0-3c148ad79bb3" width="300">|
| `scene Hunter_shop`| <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/d31771d6-d1f9-4fd3-9137-608c8198d9b0" width="300">|
| `scene bg_milk_cl`| <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/b5eac110-adb6-4479-882d-60e8b0ff95f5" width="300"> |
| `scene bg_milk_op`| <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/232ea222-cbcb-4da6-8cc4-0d8e64bc8fe4" width="300"> |
| `scene manor_sunset`| <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/9d65e1fd-a418-4d3a-ab5d-99a461c76184" width="300"> |
| `scene bg_street`| <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/e87ebb5a-5656-4175-aa72-8bc5a185dd54" width="300"> |

# Иллюстрации
Иллюстрации из игры представлены в таблице ниже:

| Код             | Предпросмотр   |
| ----------------| ---------------------------------------------------------------------------------------------------------------------- |
| `scene Teplohod_1` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/334b4f90-7961-4e04-8638-e29e1fe2a42d" width="300"> |
| `scene Teplohod_2` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/b95df110-0080-4ab8-8528-ba937fd776f2" width="300"> |
| `scene Teplohod_3` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/0958ce66-ff7c-457f-b95e-55acbb9e3d6e" width="300"> |
| `scene Teplohod_4` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/7d02c44b-f87b-41dd-b598-6dc79324c95c" width="300"> |
| `scene kas_stroking_sc` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/8a0f7ef3-9356-4fe8-966e-c4be8a783d0e" width="300"> |
| `scene Scarlett_run` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/7520aa29-2877-4c55-b0cd-d7d2c118ec5c" width="300"> |
| `scene maf_walk_n` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/80702944-e4b1-4fa6-95d3-89cfd6ee2353" width="300"> |
| `scene maf_walk_s` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/87ac4012-955e-48d8-b727-72b7de2794ce" width="300"> |
| `scene ayla_walk_1` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/d94b1436-0e4f-405a-83ca-4de29bffee41" width="300"> |
| `scene ayla_walk_2` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/5dd297e3-1aa3-418d-8483-a9897ddad6cf" width="300"> |
| `scene ayla_walk_3` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/d13af4b2-9d0b-4353-a437-d20923c2932f" width="300"> |
| `scene ayla_walk_4` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/3731086d-1e9f-4e4a-bf4b-6c084487763f" width="300"> |
| `scene maf_food`| <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/53616493-4319-44d7-aea1-db399dcf659b" width="300"> |


# Спрайты
Спрайт вызывается с помощью команды: "show <Имя спрайта>".

*Обычно*(Но не всегда) имена спрайтов состоят из слов, разделенных пробелом, включающих имя персонажа, его эмоцию и одежду. `<имя персонажа> <эмоция> <одежда>` Например: "ann smile sport" или "pavel angry short".

*НО*,В нашей новелле мы сделали проще, все спрайты у нас полноценны, то есть не разделенные на части.

Таблица со спрайтами:

Спрайты типа:
 - `close`
____________________________

| код                   | Предпросмотр    |
|-----------------------|-----------------|
| `show maf maf_cl_1`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/3e680c2a-5d62-4c1b-b12d-6cb63463f098" width="150">
| `show maf maf_cl_2`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/ec31e694-9aeb-4d4e-9534-d1cb869f3352" width="150">
| `show maf maf_cl_3`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/43d8a9c6-926a-45eb-90ee-ed90136b8727" width="150">
| `show maf maf_cl_4`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/1123b5a9-39bb-490c-9d4a-3af539cd8c93" width="150">
| `show maf maf_cl_5`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/c7d65d82-955f-42d0-9160-360de82a8cf8" width="150">
| `show maf maf_cl_6`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/2cef77e0-9b3e-4d6f-8aa5-eb8b30732ebd" width="150">
| `show maf maf_cl_7`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/368f9049-351c-48f8-b222-08da87f08951" width="150">
| `show maf maf_cl_8`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/88715715-ab7c-47fb-9387-b1882dc1ce87" width="150">
| `show maf maf_cl_9`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/a4cdc9e4-e412-4e89-bcef-bc27309ac2df" width="150">
| `show maf maf_cl_10`    | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/a49a344c-a35b-487f-bc28-46110df11ee9" width="150">
| `show maf maf_cl_11`    | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/e7de81f7-aad4-477a-8af0-b6d608dc579a" width="150">
| `show sc scrl_hun_cl_1` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/e85fbdf7-c6fd-4c48-8397-7d32422587d3" width="150">
| `show sc scrl_hun_cl_2` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/43a14dd8-3da6-47b5-8e92-2d748fee1224" width="150">
| `show sc scrl_hun_cl_3` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/883561cb-01b2-43e1-8aa5-f225a533448a" width="150">
| `show sc scrl_hun_cl_4` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/3d90ffbb-1840-4301-a8fd-136531777c03" width="150">
| `show sc scrl_hun_cl_5` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/be6ceaff-b40d-42de-882c-d4007f31f917" width="150">
| `show sc scrl_hun_cl_6` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/4f28e1d9-abf7-4391-8bfe-3d09d4d90e33" width="150">
| `show sc scrl_hun_cl_7` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/dd7551db-2620-45e0-b5a1-40a04f5f0763" width="150">
| `show sc scrl_hun_cl_8` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/b5eaf5ae-b27f-4ac1-853c-09f341c39853" width="150">
| `show sc scrl_hun_cl_9` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/d43072e5-fff7-4a06-b0b9-b74e072db4a1" width="150">
| `show sc scrl_hun_cl_10` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/9683b079-68cd-4341-a3cc-76e0bf2bde14" width="150">
| `show sc scrl_hun_cl_11` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/ccd544d3-155a-440d-8167-2cf425a03fa0" width="150">

- `far`

| код                       | Предпросмотр    |
|---------------------------|-----------------|
| `show maf maf_far_1`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/a79ca319-5b68-45d8-9495-3ab2944c57b0" width="150"> |
| `show maf maf_far_2`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/8b4a4055-428d-4b11-9707-32df86c3a3e2" width="150"> |
| `show maf maf_far_3`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/6fa3f75b-6a41-4ef1-9376-d16e157abefd" width="150"> |
| `show maf maf_far_4`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/0ad0f331-4af9-4063-9d65-2a1e3a2262f1" width="150"> |
| `show maf maf_far_5`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/a332ab9d-7d6f-4155-a5ba-656259a99158" width="150"> |
| `show maf maf_far_6`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/dcf1bedc-91d1-4580-ad5e-4cfb40ef825e" width="150"> |
| `show maf maf_far_7`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/75763bbf-7412-4f1f-8396-7489faeee867" width="150"> |
| `show maf maf_far_8`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/7c2d5afe-fc79-4692-81b7-1065851192ab" width="150"> |
| `show maf maf_far_9`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/c9d87b96-bf09-4cf6-ba65-10547f31fae8" width="150"> |
| `show maf maf_far_10`    | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/7edd7a79-3b4f-4404-b803-0fd55021d7da" width="150"> |
| `show sc scrl_hun_far_1` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/a4411031-625b-4777-a80d-29f25eca7233" width="150"> |
| `show sc scrl_hun_far_2` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/66d6bbec-0bc8-40d9-80e3-594c1a0fcff9" width="150"> |
| `show sc scrl_hun_far_3` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/5d186026-8e35-46cd-96f2-bea81792d042" width="150"> |
| `show sc scrl_hun_far_4` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/b0fe6409-3b14-4fb6-b9b9-cf73d757f5be" width="150"> |
| `show sc scrl_hun_far_5` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/b750be49-5c2f-42fe-a80e-530081e9e9cb" width="150"> |
| `show sc scrl_hun_far_6` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/aa3323fc-3157-4d6d-9525-a2e3cebede37" width="150"> |
| `show sc scrl_hun_far_7` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/dd8c1e3e-02a1-41f1-8bad-ce51bc735ee9" width="150"> |
| `show sc scrl_hun_far_8` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/267972fe-4713-48aa-af74-91b9f5ac0e74" width="150"> |
| `show sc scrl_hun_far_9` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/dfb26b9e-4c3d-48a1-a8cf-b3ada60c33d6" width="150"> |
| `show sc scrl_hun_far_10`| <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/adc9af1f-d1cf-4478-a17d-3ae9d8de9623" width="150"> |
| `show sc scrl_hun_far_11`| <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/51875d10-4dc2-4693-8449-17ee600b9fa4" width="150"> |

- `normal`

| код                       | Предпросмотр    |
|---------------------------|-----------------|
| `show maf maf_norm_1`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/a51b95dd-c46b-44e2-b0eb-27f2fd5bbdcc" width="150"> |
| `show maf maf_norm_2`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/2104db94-ae3c-466c-97ca-07a321efbf97" width="150"> |
| `show maf maf_norm_3`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/59684436-1964-414b-bc1d-989ed4a4b3f8" width="150"> |
| `show maf maf_norm_4`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/e4dcf53f-6c8b-4a04-8a3e-f18017bfa8b2" width="150"> |
| `show maf maf_norm_5`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/324e0f08-7daf-482d-8017-a4e667d65f7e" width="150"> |
| `show maf maf_norm_6`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/1f7bcca1-4dce-478e-aaa8-3247a14f0466" width="150"> |
| `show maf maf_norm_7`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/7801df3d-47d1-4934-a521-5b437930c908" width="150"> |
| `show maf maf_norm_8`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/a2d0e285-9b15-4db7-b3ec-eedf8be1f930" width="150"> |
| `show maf maf_norm_9`     | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/d3293642-b462-49ed-97a0-088d57eb0639" width="150"> |
| `show maf maf_norm_10`    | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/56a38f01-5b0d-413c-b97d-8b5469e6c0d0" width="150"> |
| `show sc scrl_hun_norm_1` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/5c198b16-6bd6-4e46-b80f-25fb02537aff" width="150"> |
| `show sc scrl_hun_norm_2` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/1509fe3d-9bd1-4d21-a856-ab1e93c0e2c7" width="150"> |
| `show sc scrl_hun_norm_3` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/aa17b70c-7cf0-41b8-8164-cf24fb74e06a" width="150"> |
| `show sc scrl_hun_norm_4` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/1450c699-0b9f-49b0-96a1-cb0b953016b0" width="150"> |
| `show sc scrl_hun_norm_5` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/346fa7ed-a289-42aa-8650-4c01fdbe7956" width="150"> |
| `show sc scrl_hun_norm_6` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/eda75b6a-a756-4628-b50e-2223c40a72a9" width="150"> |
| `show sc scrl_hun_norm_7` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/c2d219ed-f4bb-40f6-a5c4-40e533987c34" width="150"> |
| `show sc scrl_hun_norm_8` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/a9348f0a-cf0f-4ad5-b0d4-b68ed4edd9d3" width="150"> |
| `show sc scrl_hun_norm_9` | <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/37ee14b6-4606-40b4-bdd9-184742d8ddd6" width="150"> |
| `show sc scrl_hun_norm_10`| <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/77ef6c78-406d-4add-a4b8-90a2fb9f4faa" width="150"> |
| `show sc scrl_hun_norm_11`| <img src="https://github.com/RoSHaX/Kelrarium-guid-/assets/135022625/83f6a052-da55-4472-8020-ba046ce18438" width="150"> |


# Анимации появления
Мы можем плавно показывать спрайты, фоны (bg) и иллюстрации (cg), добавляя некоторую задержку между их появлением с помощью команды "with dissolve". Это даёт более естественный эффект, чем простое мгновенное появление элементов на экране.

Команда для плавности при вызове новой сцены выглядит следующим образом: 

scene <название> with <атрибут>

Здесь атрибутом может выступать, например, "dissolve", что создаст плавное появление новой сцены на экране. Также можно использовать другие атрибуты для изменения скорости, направления и т.д.

Всего атрибутов в игре 4:

- `dissolve` - Стандартный переход Ren'py, оптимален для смены BG/CG.

- `dissolve2` - 2 сек - хороший вариант для длинных переходов между локациями.

- `dissolve1` - переход с длительностью в 1 секунду, используется для создания эффекта несколько более долгой задержки при смене сцен, например может сделать поведение персонажей более естественным.

- `dissolve_fast` - 0.3 сек. используеться для более быстрого исчезнавения изображения, Используется, например, для создания эффекта "убежал" или "спрятался".

Также можно группировать несколько объектов для одновременного начала эффекта:

```Ren'py
scene Port_day
show show sc scrl_hun_norm_5
with dissolve1

```

Если в сюжете вашего мода не хватает имеющихся фоновых изображений, BG, CG и спрайтов, вы можете добавить свои.

Для этого необходимо сначала объявить изображение в блоке Init, используя переменную Image.

Например, если есть изображение forest.png, расположенное в папке game/cellars/my_mod/forest.png, то объявить его можно следующим образом:

```Ren'py
init:
    image bg les = "game/cellars/my_mod/forest.png"
```
Используем:

```Ren'py
label my_mod:
    scene bg les with dissolve
```

- Я настоятельно рекомендую использовать теги. В данном примере, слово "bg" выступает в качестве тега для изображения. Если объявить несколько фоновых изображений с таким же тегом, то при показе следующего изображения оно автоматически заменит предыдущее.

Кроме того, возможна создание анимации с использованием изображений. Подробнее об этом вы можете узнать на [странице документации](https://www.renpy.org/doc/html/atl.html)

# Звуки

"Ren'Py поддерживает воспроизведение музыки и звуковых эффектов, используя следующие форматы аудио файлов: Opus, Ogg Vorbis, mp3, wav."

- # Добавление звуков, музыки, эмбиенса

Объявление аудиофайла происходит следующим образом:

- `$ <Название аудиофайла> = <Путь к аудиофайлу>`

Для добавления различных аудиофайлов в ваш мод используйте команду, приведенную выше. Рассмотрим пример ее использования.

```Ren'py
init:
    $ forest = "cellars/sounds/forest_ambience.mp3"

label my_mod_1:
    play ambience forest # Проигрываем эмбиенс леса на канале `ambience`

```

- Для проигрывания музыки используется: play music <Название>, а для остановки - stop music.

Список музыки:

| код                                  | Название                  |
|--------------------------------------|---------------------------|
| play music music_list["Infinity"]    | Artem Zebrev - Infinity   |
| play music music_list["Gray_Man"]    | Artem Zebrev - Gray_Man   |
| play music music_list["Kelt_reliz"]  | Artem Zebrev - Kelt_reliz |

- Для проигрывания звуков окружения(Например пение птиц, или шум воды) используется: play ambient <Название>, остановка - stop ambient.

Список звуков окружение:

| код                                     | описание                  |
|-----------------------------------------|---------------------------|
| play ambient ambient_list["port"]       | Морской порт.             |
| play ambient ambient_list["settlement"] | Посёлок(Птицы,кузнеца...) |


- Для проигрывания прочих звуков(Глоток воды, закрывшаяся дверь и т.п) используется: play sound <Название>, остановка - stop sound.

Список звуков:

| код                                  | описание                  |
|--------------------------------------|---------------------------|
| play sound sfx_list["drink"]         | Глоток воды.              |
| play sound sfx_list["shlepok"]       | Пощёчина.                 |
| play sound sfx_list["tifon"]         | Гудок теплохода.          |

# Плавный вход/выход музыки

Для создания плавного входа и выхода музыки вы можете использовать команды "fadein" и "fadeout".

- Обратите внимание, что эти команды не являются обязательными. Команда "fadeout" задает время затухания для текущей проигрываемой музыки (в секундах).

А команда "fadein" определяет время, необходимое для плавного "входа" новой музыки.

```Ren'py
label my_mod:
    play ambient "sounds/ambient/the_port.mp3" # Воспроизведение музыки с "входом" в 4 секунды
    '...' # Происходят какие-то действия по сюжету
    stop ambient fadeout 4 # Остановка музыки с затуханием в 4 секунды
```

# Зацикливание и разцикливание музыки
Команды "loop" и "noloop" также не являются обязательными.

Команда "loop" заставляет музыку зацикливаться, а "noloop" - играть только один раз. Если ни одна из указанных команд не задана, то значение канала будет использоваться по умолчанию.

```Ren'py
label my_mod:
    play sound "sounds/ambient/tifon.mp3" loop # Зацикливаем звук гула коробля
    play music music_list["Gray_Man"] noloop # Разцикливаем музыку, заставляя её играть только один раз
```

# Видео

Ren'Py может использовать FFmpeg (в комплекте) для воспроизведения фильмов с использованием видеокодеков: WebM, Matroska, Ogg, AVI.

- Полноэкранные видеоролики

Для отображения видео в полноэкранном режиме можно использовать функцию 
`renpy.movie_cutscene`. Она проигрывает видео в полноэкранном режиме до конца либо до тех пор, пока игрок не нажмет на кнопку мыши, чтобы прекратить воспроизведение.

Это самый простой способ отображения видео в полноэкранном режиме.

```Ren'py
label my_mod:
    "Смотрим мультик!"
    $ renpy.movie_cutscene("Зверополис.webm")
    "Мультик закончился."
```

Также можно использовать видео, как отображаемые объекты и спрайты.
Но об этом можно узнать [тут](https://www.renpy.org/doc/html/movie.html)


_______________________________________________________
Спасибо, что прочитали данное руководство! Надеюсь, оно было полезным для вас. Если у вас есть какие-либо вопросы или комментарии, не стесняйтесь обращаться ко [мне](https://vk.com/rosha586). Буду рад вам помочь!

P.S Статья будет регулярно обновляться вместе с обновлениями игры!
