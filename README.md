# ПР01 — окружение и граф ROS 2

Работа проведена в Ubuntu 24.04 / ROS 2 Jazzy внутри Docker. Стандартный `turtlesim_node` и `turtle_teleop_key` запускались в виртуальном X-дисплее; клавиши стрелок отправлены в псевдотерминал teleop. Исходный домен — 216, соседний — 217. На занятии эти значения заменяются на выделенную пару.

Код воспроизводимого опыта: [capture_pr01.py](tools/capture_pr01.py). Из терминала с ROS 2 и установленными `turtlesim`/`Xvfb`:

```bash
source /opt/ros/jazzy/setup.bash
PR01_DOMAIN_ID=216 python3 tools/capture_pr01.py
```

Фактические результаты и команды приведены в [graph.md](evidence/pr01/graph.md); версии среды — в [environment.json](evidence/pr01/environment.json), полный `ros2 doctor --report` — в [doctor.txt](evidence/pr01/doctor.txt). В исходном домене измерена частота `/turtle1/pose` 62,496 Гц. В соседнем домене CLI не увидел симулятор и получил таймаут, после возврата в исходный домен снова получил позу.

Архив course kit хранится вне этого репозитория: `../.course-kit/v1` при работе в текущей папке. Проверка из корня этой работы:

```bash
python3 ../.course-kit/v1/tools/check_practice.py PR01 --submission .
```

Декларация использования ИИ: [AI_USAGE.md](AI_USAGE.md). Для проверки ПР01 используйте тег `pr01-submission`: `report.commit` указывает на коммит реализации перед добавлением evidence.

## ПР02 — пакет и запуск turtlesim

Пакет [turtle_bringup](src/turtle_bringup/package.xml) устанавливает [sim.launch.py](src/turtle_bringup/launch/sim.launch.py) для запуска готовой ноды `turtlesim_node`. Сборка и запуск из корня репозитория:

```bash
source /opt/ros/jazzy/setup.bash
colcon build --symlink-install --packages-select turtle_bringup
source install/setup.bash
ros2 launch turtle_bringup sim.launch.py
```

Пустой пакет был собран до добавления launch-файла. Логи обеих сборок, команды и результаты опыта находятся в [evidence/pr02](evidence/pr02/). При публикации `Twist` в `/cmd_vel` подписчиков не было и поза черепашки не менялась. После публикации в `/turtle1/cmd_vel` появился подписчик, а поза изменилась. Сценарий для повторения: [capture_pr02.py](tools/capture_pr02.py).

Для проверки ПР02 на теге `pr02-submission`:

```bash
python3 -m py_compile src/turtle_bringup/launch/sim.launch.py
python3 ../.course-kit/v1/tools/check_practice.py PR02 --submission .
```

[CI](.github/workflows/ros.yml) собирает пакет в ROS 2 Jazzy и проверяет установленный launch-файл. ПР01 следует проверять на её теге, потому что контракт course kit допускает после коммита реализации только evidence соответствующей работы.
