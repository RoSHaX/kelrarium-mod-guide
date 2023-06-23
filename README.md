<h1 align="center">Кельрариум - Гайд по созданию модов.</h1>
<h1 aligh="center"><img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/b866985e-35e2-4f2e-abb5-252b1f425adf" width="1280"></h1>

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
| `scene Misly`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/fa68d205-d8f7-4c78-b8ec-7f1732fd736b" width="300">|
| `scene Port_day`  | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/faa530fd-620a-4666-9b6d-ddcfb54c1293" width="300">|
| `scene Hunter_shop`| <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/4af7002c-233e-4710-b5ff-77a10044366e" width="300">|
| `scene bg_milk_cl`| <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/9e8d3584-4714-403a-a400-b20c40196581" width="300"> |
| `scene bg_milk_op`| <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/ac80628c-4d3e-406a-a69f-20b4bdcb43c3" width="300"> |
| `scene manor_sunset`| <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/53f3a798-5276-4cd3-9351-71f8d14a0efe" width="300"> |
| `scene bg_street`| <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/88e991e1-c685-4f88-a26f-4909e923f705" width="300"> |

# Иллюстрации
Иллюстрации из игры представлены в таблице ниже:

| Код             | Предпросмотр   |
| ----------------| ---------------------------------------------------------------------------------------------------------------------- |
| `scene Teplohod_1` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/5c72530e-b3ce-4ea1-b441-34bd49957c2c" width="300"> |
| `scene Teplohod_2` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/122b826f-bd0a-4364-8137-91a104a127ce" width="300"> |
| `scene Teplohod_3` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/43283628-ab57-4372-a023-7d09141829c1" width="300"> |
| `scene Teplohod_4` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/0203fd86-4509-45e8-a677-c3c3900d8832" width="300"> |
| `scene kas_stroking_sc` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/167d917f-ff6e-488a-90ed-dc9f6fba19e1" width="300"> |
| `scene Scarlett_run` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/2aed1f67-eaba-461b-b4ca-7b44138804b8" width="300"> |
| `scene maf_walk_n` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/cb3f2485-fcac-4730-93e4-728242b0b9d3" width="300"> |
| `scene maf_walk_s` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/eccafb02-7a2f-4709-970c-8b2c1a586ec0" width="300"> |
| `scene ayla_walk_1` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/7aa7baf4-3b78-40dd-aa1b-6076ce9953a7" width="300"> |
| `scene ayla_walk_2` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/6af4ac52-5199-497c-b33d-77730b17923e" width="300"> |
| `scene ayla_walk_3` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/9c9662eb-66f3-47d1-8b05-6d4a82bd5719" width="300"> |
| `scene ayla_walk_4` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/392ca624-1b80-4600-9f60-5732f973813c" width="300"> |
| `scene maf_food`| <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/8289daf4-63f2-428d-bc7e-15bd61405f5f" width="300"> |


# Спрайты
Спрайт вызывается с помощью команды: "show <Имя спрайта>".

*Обычно*(Но не всегда) имена спрайтов состоят из слов, разделенных пробелом, включающих имя персонажа, его эмоцию и одежду. `<имя персонажа> <эмоция> <одежда>` Например: "ann smile sport" или "pavel angry short".

Но,В нашей новелле мы сделали проще, все спрайты у нас полноценны, то есть не разделенные на части.

Таблица со спрайтами:

Спрайты типа:
 - `close`
____________________________

| код                   | Предпросмотр    |
|-----------------------|-----------------|
| `show maf maf_cl_1`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/23ef72f5-4567-40e4-9bf0-68767a866dae" width="150">
| `show maf maf_cl_2`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/170374c5-d748-4e67-b255-fa5d2b3d3443" width="150">
| `show maf maf_cl_3`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/2fbb0e5f-3554-4d76-98c5-78a437c22fef" width="150">
| `show maf maf_cl_4`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/ed09af33-6f13-432f-bfb1-496a429aa23c" width="150">
| `show maf maf_cl_5`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/587ea7d2-7cff-4264-ac12-b983403a0177" width="150">
| `show maf maf_cl_6`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/6be27f87-0905-4f81-a8dc-ed48eb879474" width="150">
| `show maf maf_cl_7`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/64393847-da38-4c05-afcb-bb35373bbe74" width="150">
| `show maf maf_cl_8`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/99a670e1-b92d-408d-9880-2da345306426" width="150">
| `show maf maf_cl_9`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/dde0b0e7-50ab-4a19-89ab-7634887e095c" width="150">
| `show maf maf_cl_10`    | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/8fd68002-51cd-4a78-a683-540d8dde4df6" width="150">
| `show maf maf_cl_11`    | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/6b1fb763-b052-431a-a12b-d18a5f3618f3" width="150">
| `show sc scrl_hun_cl_1` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/b8a148bb-b531-4583-a84e-4021e9ae41ac" width="150">
| `show sc scrl_hun_cl_2` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/479314da-74f7-452a-91c5-6561068a1192" width="150">
| `show sc scrl_hun_cl_3` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/3194cbde-8704-422e-8e26-7433b31888ea" width="150">
| `show sc scrl_hun_cl_4` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/33ea546a-1652-4f98-891b-9d4a11037918" width="150">
| `show sc scrl_hun_cl_5` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/aba25f7d-d030-42ac-b7d9-af8cc1e69448" width="150">
| `show sc scrl_hun_cl_6` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/2bef60ed-404f-41d8-b153-e116c9f886ca" width="150">
| `show sc scrl_hun_cl_7` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/e344e61a-f523-4d15-b95f-c619ad206334" width="150">
| `show sc scrl_hun_cl_8` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/0e95aa3a-1976-4ce5-94f5-6a429592e867" width="150">
| `show sc scrl_hun_cl_9` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/793fcfc8-7a1a-4128-a97f-3cc6c44a7602" width="150">
| `show sc scrl_hun_cl_10` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/f0b6e43e-38a4-4e4f-93ea-1bd59ac85028" width="150">
| `show sc scrl_hun_cl_11` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/1ec6fd97-65ed-4106-aad6-5a632f6c9c4f" width="150">

- `far`

| код                       | Предпросмотр    |
|---------------------------|-----------------|
| `show maf maf_far_1`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/6def1713-6e5d-4599-be92-e3e2ea58b557" width="150"> |
| `show maf maf_far_2`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/3cebb546-8f5f-460d-9938-427f7cc70838" width="150"> |
| `show maf maf_far_3`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/f405ae97-45e8-4545-b568-397ea0bf1f11" width="150"> |
| `show maf maf_far_4`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/4353246e-2743-48fd-a01f-fc2e72fcf1dd" width="150"> |
| `show maf maf_far_5`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/d79f224d-084c-4937-9068-6ec626dd4134" width="150"> |
| `show maf maf_far_6`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/1f49a66c-3758-457f-aac2-9a47a7eb90ef" width="150"> |
| `show maf maf_far_7`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/42605e8a-ed3b-4909-b2d0-2e8b9f6bd57a" width="150"> |
| `show maf maf_far_8`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/c151d88c-029d-483b-891a-70d4cc2d9f0b" width="150"> |
| `show maf maf_far_9`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/dae0addb-9523-40c0-88d8-f4458053d9d3" width="150"> |
| `show maf maf_far_10`    | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/bc0f142c-0d94-4f21-8ddc-0558bab79438" width="150"> |
| `show sc scrl_hun_far_1` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/50faed94-ae18-4ab9-bd95-2697281a45dd" width="150"> |
| `show sc scrl_hun_far_2` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/91cf688e-9bad-49bd-99fa-f6788020792e" width="150"> |
| `show sc scrl_hun_far_3` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/8dbd3582-0994-4d91-9f33-086e0f77034c" width="150"> |
| `show sc scrl_hun_far_4` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/2963e7be-438e-45aa-99c6-df5d5ba2c1fe" width="150"> |
| `show sc scrl_hun_far_5` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/cae06a26-b297-4e4d-846d-f48edb279af3" width="150"> |
| `show sc scrl_hun_far_6` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/1c3ef50c-ca77-4084-8ee7-e656000d88b8" width="150"> |
| `show sc scrl_hun_far_7` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/f3b2d477-cf5a-440b-a44e-a881d12d8be9" width="150"> |
| `show sc scrl_hun_far_8` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/3375a8e2-2f40-45ec-8ba9-93a5b1425068" width="150"> |
| `show sc scrl_hun_far_9` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/c7219cbe-a58f-4516-8100-ed1322ab4594" width="150"> |
| `show sc scrl_hun_far_10`| <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/816b4e74-cbea-42ae-bea5-f15d07433b61" width="150"> |
| `show sc scrl_hun_far_11`| <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/3086c174-bf7f-4f02-8921-488baa4494e2" width="150"> |

- `normal`

| код                       | Предпросмотр    |
|---------------------------|-----------------|
| `show maf maf_norm_1`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/b59104a6-6ec6-4154-946d-94b90229c571" width="150"> |
| `show maf maf_norm_2`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/f348e7fc-0058-4829-b03c-58e1f5d281c4" width="150"> |
| `show maf maf_norm_3`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/445a84b0-43f4-44f7-b2ca-acbd3532231a" width="150"> |
| `show maf maf_norm_4`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/f224bf71-f62e-4734-8c89-e60c30b94743" width="150"> |
| `show maf maf_norm_5`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/e47e8624-93af-4152-8c93-434e389ef8a5" width="150"> |
| `show maf maf_norm_6`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/770eb035-746e-45c3-9950-bb2fd17c1c49" width="150"> |
| `show maf maf_norm_7`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/5d40c57c-94f8-4805-adec-96d73deb2f05" width="150"> |
| `show maf maf_norm_8`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/c1da87e0-0bdb-47a3-8f6c-8edc50c48949" width="150"> |
| `show maf maf_norm_9`     | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/eee8a648-96b9-4712-982f-b6cbe654fafb" width="150"> |
| `show maf maf_norm_10`    | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/498fbab4-83f6-4c5a-b1fb-3ce9e0e8e44e" width="150"> |
| `show sc scrl_hun_norm_1` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/a0468f54-9b63-4ff0-afc4-f9968169c542" width="150"> |
| `show sc scrl_hun_norm_2` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/3ad89355-ec19-4d6f-963b-888acbc9555c" width="150"> |
| `show sc scrl_hun_norm_3` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/58db232c-9ce1-41b3-8eb9-2441dc8f7be2" width="150"> |
| `show sc scrl_hun_norm_4` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/eb115907-d3d2-468b-ad21-e4d4efb3c5c9" width="150"> |
| `show sc scrl_hun_norm_5` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/2f9e096f-cbe6-48fe-a6e4-e5d26557bf92" width="150"> |
| `show sc scrl_hun_norm_6` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/7f89e34c-dce3-4785-a813-bf42e5036494" width="150"> |
| `show sc scrl_hun_norm_7` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/5401e18f-2579-4f24-9e75-658ea1725baf" width="150"> |
| `show sc scrl_hun_norm_8` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/8a1e2171-6f44-4c57-9e5c-d5b75040d209" width="150"> |
| `show sc scrl_hun_norm_9` | <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/4e33d530-4918-451d-81df-90661975df69" width="150"> |
| `show sc scrl_hun_norm_10`| <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/bb36bb65-8186-4af3-8bf4-41da09b80c65" width="150"> |
| `show sc scrl_hun_norm_11`| <img src="https://github.com/RoSHaX/kelrarium-mod-guide/assets/135022625/7ff89e9a-4a4f-4974-a619-05d57ffa7448" width="150"> |


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
