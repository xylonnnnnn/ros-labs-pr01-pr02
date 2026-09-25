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
