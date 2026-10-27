1. read_valid_param(prompt, min_val, max_val) — циклический запрос и валидация одного числа в
границах;
 2. calc_oil_volume(q_liq, w_pct) — расчёт объёмного дебита нефти Qн = Qж * (1 - W / 100);
• 3. calc_oil_mass(q_oil, density) — перевод объёма нефти в тонны Mн = Qн * плотность / 1000;
 4. evaluate_profitability(m_oil, m_min) — классификация статуса рентабельности через if-elif-else.
```mermaid
flowchart TD
 Start([Начало работы]) --> InputQ[/Ввод Qж и W с валидацией границ/]
 InputQ --> CheckValid{Значения в пределах\nQж: 0..1000, W: 0..100?}
 CheckValid -- Нет --> ErrMsg[/Вывод ошибки диапазона/]
 ErrMsg --> InputQ
 CheckValid -- Да --> CalcVol[Расчёт объёма нефти:\nQн = Qж * 1 - W/100]
 CalcVol --> CalcMass[Расчёт массы нефти:\nMн = Qн * 850 / 1000]
 CalcMass --> Cond1{Mн < M_min?}
 Cond1 -- Да --> Status1[Статус: Убыточна - стоп]
 Cond1 -- Нет --> Cond2{Mн < 3 * M_min?}
 Cond2 -- Да --> Status2[Статус: Рентабельна - база]
 Cond2 -- Нет --> Status3[Статус: Высокодебитная - приоритет]
 Status1 --> Output[/Вывод сводки: Qн, Mн, Статус/]
 Status2 --> Output
 Status3 --> Output
 Output --> End([Конец работы])
```
