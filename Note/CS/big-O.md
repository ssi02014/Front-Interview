# π» λΉμ€(Big-O)νκΈ°λ²
<br />

## π¨π»βπ» λΉμ€(Big-O)λ?
- λΉμ€(O, Big-O)λ μλ ₯κ°μ΄ λ¬΄νλλ‘ ν₯ν λ ν¨μμ μνμ μ€λͺνλ μνμ  νκΈ° λ°©λ²μ΄λ€.
- μ»΄ν¨ν° κ³Όνμμ λΉμ€λ μλ ₯κ°μ΄ μ»€μ§ λ μκ³ λ¦¬μ¦μ `μ€ν μκ°(μκ° λ³΅μ‘λ)`κ³Ό ν¨κ» `κ³΅κ° μκ΅¬μ¬ν­(κ³΅κ° λ³΅μ‘λ)`μ΄ μ΄λ»κ² μ¦κ°νλμ§λ₯Ό λΆλ₯νλ λ° μ¬μ©λλ€.
- μκ³ λ¦¬μ¦μ ν¨μ¨μ±μ λΆμνλ λ°μλ λ§€μ° μ μ©νκ² νμ© λλ€.
- μκ³ λ¦¬μ¦μ νν 'μκ°κ³Ό κ³΅κ°μ΄ νΈλ μ΄λ μ€ν(Space-Time Tradeoff)' κ΄κ³λ€. μ΄ λ§μ μ€ν μκ°μ΄ λΉ λ₯Έ μκ³ λ¦¬μ¦μ κ³΅κ°μ λ§μ΄ μ¬μ©νκ³ , κ³΅κ°μ μ κ² μ°¨μ§νλ μκ³ λ¦¬μ¦μ μ€ν μκ°μ΄ λλ¦¬λ€λ μ΄μΌκΈ°μ΄λ€.


<br />

## π¨π»βπ» μκ° λ³΅μ‘λ(Time Complexity)
- μκ° λ³΅μ‘λμ μ¬μ μ  μ μλ μ΄λ€ μκ³ λ¦¬μ¦μ μννλ λ° κ±Έλ¦¬λ μκ°μ μ€λͺνλ κ³μ° λ³΅μ‘λ(Computational Complexity)λ₯Ό μλ―Ένλ©°, κ³μ° λ³΅μ‘λλ₯Ό νκΈ°νλ λνμ μΈ λ°©λ²μ΄ λ°λ‘ λΉμ€λ€.
- λΉμ€λ‘ μκ° λ³΅μ‘λλ₯Ό ννν  λλ μ΅κ³ μ°¨ν­λ§μ νκΈ°νλ©°, κ³μλ λ¬΄μνλ€. μλ₯Ό λ€μ΄ μλ ₯κ° nμ λν΄ 4n^2 + 3n + 4 λ§νΌ κ³μ°νλ ν¨μκ° μλ€λ©΄ μ΄ ν¨μμ μκ° λ³΅μ‘λλ μ΅κ³ μ°¨ν­μΈ 4n^2λ§μ κ³ λ €νλ€. μ΄μ€μμλ κ³μλ λ¬΄μνλ©° n^2 λ§μ κ³ λ €νλ€. μ¦, μκ° λ³΅μ‘λλ O(n^2)μ΄ λλ€.

<br />

## π¨π»βπ» κ³΅κ° λ³΅μ‘λ(Space Complexity)
- κ³΅κ° λ³΅μ‘λλ, νλ‘κ·Έλ¨μ μ€νμν¨ ν μλ£νλλ° νμλ‘ νλ μμ κ³΅κ°μ μμ λ§νλ€.
- μ΄ κ³΅κ° μκ΅¬ = κ³ μ  κ³΅κ° μκ΅¬ + κ°λ³ κ³΅κ° μκ΅¬λ‘ λνλΌ μ μλ€.
- κ³ μ  κ³΅κ°μ μλ ₯κ³Ό μΆλ ₯μ νμλ ν¬κΈ°μ κ΄κ³μλ κ³΅κ°μ μκ΅¬(μ½λ μ μ₯ κ³΅κ°, λ¨μ λ³μ, κ³ μ  ν¬κΈ°μ κ΅¬μ‘° λ³μ, μμ)λ₯Ό λ§νλ€.
- κ°λ³ κ³΅κ°μ ν΄κ²°νλ €λ λ¬Έμ μ νΉμ  μΈμ€ν΄μ€μ μμ‘΄νλ ν¬κΈ°λ₯Ό κ°μ§ κ΅¬μ‘°ν λ³μλ€μ μν΄μ νμλ‘ νλ κ³΅κ°, ν¨μκ° μν νΈμΆμ ν  κ²½μ° μκ΅¬λλ μΆκ° κ³΅κ°, μ¦ λμ μΌλ‘ νμν κ³΅κ°μ λ§νλ€.

<br />

## π¨π»βπ» λΉμ€ μ’λ₯
### π O(1)
- μλ ₯κ°μ΄ μλ¬΄λ¦¬ μ»€λ μ€ν μκ°μ μΌμ νλ€.
- μ΅κ³ μ μκ³ λ¦¬μ¦μ΄λΌ ν  μ μλ€.
- O(1)μ μ€νλλ μκ³ λ¦¬μ¦μΌλ‘ ν΄μ νμ΄λΈμ μ‘°ν λ° μ½μμ΄ ν΄λΉνλ€.

<br />

### π O(log n)
- O(1)κ³Ό λ€λ₯΄κ² μ€ν μκ°μ΄ μλ ₯κ°μ μν₯μ λ°λλ€.
- λ‘κ·Έλ λ§€μ° ν° μλ ₯κ°μλ ν¬κ² μν₯μ λ°μ§ μλ νΈμ΄κΈ° λλ¬Έμ μ¬λ§ν nμ ν¬κΈ°μ λν΄μλ λ§€μ° κ²¬κ³ νλ€.
- λνμ μΌλ‘ μ΄μ§ κ²μμ΄ μ΄μ ν΄λΉνλ€.

<br />

### π O(n)
- μλ ₯κ°λ§νΌ μ€ν μκ°μ μν₯μ λ°μΌλ©°, μκ³ λ¦¬μ¦μ μννλ λ° κ±Έλ¦¬λ μκ°μ μλ ₯κ°μ λΉλ‘νλ€. μ΄λ¬ν μκ³ λ¦¬μ¦μ μ ν μκ°(Linear-Time)μκ³ λ¦¬μ¦μ΄λΌκ³  νλ€.
- μ λ ¬λμ§ μμ λ¦¬μ€νΈμμ μ΅λκ° λλ μ΅μκ°μ μ°Ύλ κ²½μ°κ° μ΄μ ν΄λΉνλ©° μ΄ κ°μ μ°ΎκΈ° μν΄μλ λͺ¨λ  μλ ₯κ°μ μ μ΄λ ν λ² μ΄μμ μ΄ν΄λ΄μΌ νλ€.

<br />

### π O(n log n)
- λ³ν© μ λ ¬μ λΉλ‘―ν λλΆλΆμ ν¨μ¨ μ’μ μ λ ¬ μκ³ λ¦¬μ¦μ΄ μ΄μ ν΄λΉνλ€.
- μ μ΄λ λͺ¨λ  μμ λν΄ ν λ² μ΄μμ λΉκ΅ν΄μΌ νλ λΉκ΅ κΈ°λ° μ λ ¬ μκ³ λ¦¬μ¦μ μλ¬΄λ¦¬ μ’μ μκ³ λ¦¬μ¦λ O(n log n)λ³΄λ€ λΉ λ₯Ό μ μλ€.
- λ¬Όλ‘  μλ ₯κ°μ΄ μ΅μ μΈ κ²½μ°, λΉκ΅λ₯Ό κ±΄λ λ°μ΄ O(n)μ΄ λ  μ μμΌλ©° νμνΈ(Timesort)κ° μ΄λ° λ‘μ§μ κ°κ³  μλ€.

<br />

### π O(n^2)
- λ²λΈ μ λ ¬ κ°μ λΉν¨μ¨μ μΈ μ λ ¬ μκ³ λ¦¬μ¦μ΄ μ΄μ ν΄λΉνλ€.

<br />

### π O(2^n)
- νΌλ³΄λμΉ μλ₯Ό μ¬κ·λ‘ κ³μ°νλ μκ³ λ¦¬μ¦μ΄ μ΄μ ν΄λΉνλ€.
- n^2μ λΉμ·ν΄λ³΄μ΄μ§λ§ 2^nμ΄ ν¨μ¬ λ ν¬λ€.

<br />

### π O(n!)
- κ° λμλ₯Ό λ°©λ¬Ένκ³  λμμ€λ κ°μ₯ μ§§μ κ²½λ‘λ₯Ό μ°Ύλ μΈνμ λ¬Έμ (Travelling Salesman Problem)λ₯Ό λΈλ£¨νΈ ν¬μ€λ‘ νμ΄ν  λκ° μ΄μ ν΄λΉνλ€.
- κ°μ₯ λλ¦° μκ³ λ¦¬μ¦μΌλ‘, μλ ₯κ°μ΄ μ‘°κΈλ§ μ»€μ Έλ μ¬λ§ν λ€ν­ μκ° λ΄μλ κ³μ°κΈ° μ΄λ ΅λ€.

<br />
