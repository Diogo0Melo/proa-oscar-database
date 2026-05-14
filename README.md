# 🏆 Desafio MongoDB: Oscar Edition 🎬

[![MongoDB](https://img.shields.io/badge/Database-MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![Status](https://img.shields.io/badge/Status-resolvendo-yellow?style=for-the-badge)](#)

Este repositório contém a resolução de uma série de exercícios práticos utilizando **MongoDB Query Language (MQL)**. O objetivo é explorar uma base de dados histórica sobre as indicações e vitórias do Oscar

## 🛠️ Tecnologias e Ferramentas
*   **Banco de Dados:** MongoDB (NoSQL)
*   **Interface:** MongoDB Compass / Mongosh
*   **Dataset:** Histórico de indicados ao Oscar (1928 - 2026)

## 🗺️ Guia de Consultas

<details>
<summary><strong><h3 style="display: inline-block">📂 Nível 1: Primeiros Passos</h3></strong></summary>
<br>


<details>
<summary><strong> 1.1 Quantos registros existem na coleção de indicados ao Oscar?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.countDocuments()
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 11104 registros
```

</details>
</details>
<br>

<details>
<summary><strong>1.2 Quais são as diferentes categorias de premiação que existem no banco de dados? Liste todas as categorias únicas.</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.distinct("categoria").length
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 122 categorias diferentes
```

</details>
</details>
<br>

<details>
<summary><strong>1.3 Qual foi o primeiro ano de cerimônia do Oscar registrado na base?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.find({}, { "ano_cerimonia": 1 }).sort({ "ano_cerimonia": 1 }).limit(1)
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
{
  _id: ObjectId('6a047a36dc0838daf8ef97be'),
  ano_cerimonia: 1928
}
```

</details>
</details>
<br>

<details>
<summary><strong>1.4 Qual foi o último ano de cerimônia registrado na base?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.find({}, { "ano_cerimonia": 1 }).sort({ "ano_cerimonia": -1 }).limit(1)
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
{
  _id: ObjectId('6a04808edc0838daf8efc2c3'),
  ano_cerimonia: 2026
}
```

</details>
</details>
<br>

<details>
<summary><strong>1.5 Quantas cerimônias do Oscar estão registradas no total?</strong></summary>

💻 **Query:**
```javascript
db.oscar.distinct("cerimonia").length
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 98
```

</details>
</details>
<br>
</details>


<details>
<summary><strong><h3 style="display: inline-block">📂 Nível 2: Explorando Categorias</h3></strong></summary>
<br>

<details>
<summary><strong>🎬 2.1 Quantas indicações existem para cada categoria? Agrupe por categoria e ordene da mais frequente para a menos frequente.</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.aggregate([
  { 
    $group: { 
      _id: "$categoria", 
      quantidade: { $sum: 1 } 
    } 
  },
  { 
    $sort: { quantidade: -1 } 
  }
]).toArray()
```

<details>
<summary><strong>Ver Resposta 🕵️‍♂️🔍</strong></summary>
<br>

```json
[
  { _id: 'DIRECTING', quantidade: 479 },
  { _id: 'FILM EDITING', quantidade: 460 },
  { _id: 'ACTRESS IN A SUPPORTING ROLE', quantidade: 445 },
  { _id: 'ACTOR IN A SUPPORTING ROLE', quantidade: 445 },
  { _id: 'BEST PICTURE', quantidade: 391 },
  { _id: 'DOCUMENTARY (Short Subject)', quantidade: 378 },
  { _id: 'CINEMATOGRAPHY', quantidade: 348 },
  { _id: 'DOCUMENTARY (Feature)', quantidade: 345 },
  { _id: 'FOREIGN LANGUAGE FILM', quantidade: 315 },
  { _id: 'ART DIRECTION', quantidade: 307 },
  { _id: 'COSTUME DESIGN', quantidade: 305 },
  { _id: 'MUSIC (Original Score)', quantidade: 270 },
  { _id: 'SOUND', quantidade: 255 },
  { _id: 'ACTOR IN A LEADING ROLE', quantidade: 245 },
  { _id: 'ACTRESS IN A LEADING ROLE', quantidade: 245 },
  { _id: 'ACTRESS', quantidade: 236 },
  { _id: 'MUSIC (Original Song)', quantidade: 235 },
  { _id: 'ACTOR', quantidade: 232 },
  { _id: 'SHORT FILM (Live Action)', quantidade: 226 },
  { _id: 'MUSIC (Song)', quantidade: 215 },
  { _id: 'SHORT FILM (Animated)', quantidade: 215 },
  { _id: 'SOUND RECORDING', quantidade: 195 },
  { _id: 'SHORT SUBJECT (Cartoon)', quantidade: 169 },
  { _id: 'VISUAL EFFECTS', quantidade: 165 },
  { _id: 'CINEMATOGRAPHY (Black-and-White)', quantidade: 161 },
  { _id: 'WRITING (Original Screenplay)', quantidade: 160 },
  {
    _id: 'MUSIC (Music Score of a Dramatic or Comedy Picture)',
    quantidade: 148
  },
  { _id: 'ART DIRECTION (Black-and-White)', quantidade: 138 },
  { _id: 'CINEMATOGRAPHY (Color)', quantidade: 135 },
  { _id: 'HONORARY AWARD', quantidade: 133 },
  { _id: 'MUSIC (Scoring of a Musical Picture)', quantidade: 127 },
  {
    _id: 'WRITING (Screenplay Written Directly for the Screen)',
    quantidade: 120
  },
  { _id: 'ART DIRECTION (Color)', quantidade: 112 },
  { _id: 'WRITING (Adapted Screenplay)', quantidade: 110 },
  { _id: 'WRITING (Screenplay)', quantidade: 104 },
  { _id: 'ANIMATED FEATURE FILM', quantidade: 104 },
  { _id: 'OUTSTANDING PRODUCTION', quantidade: 102 },
  {
    _id: 'WRITING (Screenplay--based on material from another medium)',
    quantidade: 95
  },
  { _id: 'SPECIAL EFFECTS', quantidade: 93 },
  { _id: 'SHORT SUBJECT (One-reel)', quantidade: 90 },
  { _id: 'BEST MOTION PICTURE', quantidade: 90 },
  { _id: 'MAKEUP', quantidade: 87 },
  { _id: 'SOUND EDITING', quantidade: 86 },
  { _id: 'SOUND MIXING', quantidade: 85 },
  { _id: 'SHORT SUBJECT (Two-reel)', quantidade: 81 },
  { _id: 'COSTUME DESIGN (Black-and-White)', quantidade: 77 },
  { _id: 'COSTUME DESIGN (Color)', quantidade: 77 },
  { _id: 'PRODUCTION DESIGN', quantidade: 70 },
  { _id: 'SHORT SUBJECT (Live Action)', quantidade: 68 },
  {
    _id: 'WRITING (Screenplay Based on Material from Another Medium)',
    quantidade: 65
  },
  { _id: 'MUSIC (Scoring)', quantidade: 64 },
  {
    _id: 'WRITING (Story and Screenplay--written directly for the screen)',
    quantidade: 60
  },
  { _id: 'SPECIAL AWARD', quantidade: 56 },
  { _id: 'MAKEUP AND HAIRSTYLING', quantidade: 56 },
  {
    _id: 'WRITING (Screenplay Based on Material Previously Produced or Published)',
    quantidade: 55
  },
  { _id: 'WRITING (Original Story)', quantidade: 52 },
  { _id: 'WRITING (Motion Picture Story)', quantidade: 50 },
  { _id: 'SOUND EFFECTS EDITING', quantidade: 47 },
  { _id: 'IRVING G. THALBERG MEMORIAL AWARD', quantidade: 45 },
  { _id: 'JEAN HERSHOLT HUMANITARIAN AWARD', quantidade: 44 },
  { _id: 'MUSIC (Original Dramatic Score)', quantidade: 41 },
  { _id: 'ASSISTANT DIRECTOR', quantidade: 35 },
  { _id: 'WRITING (Story and Screenplay)', quantidade: 35 },
  { _id: 'INTERNATIONAL FEATURE FILM', quantidade: 35 },
  {
    _id: 'MUSIC (Scoring of Music--adaptation or treatment)',
    quantidade: 30
  },
  { _id: 'OUTSTANDING MOTION PICTURE', quantidade: 30 },
  { _id: 'WRITING (Original Motion Picture Story)', quantidade: 25 },
  { _id: 'DOCUMENTARY', quantidade: 25 },
  { _id: 'MUSIC (Song--Original for the Picture)', quantidade: 25 },
  { _id: 'DANCE DIRECTION', quantidade: 21 },
  {
    _id: 'WRITING (Story and Screenplay--based on factual material or material not previously published or produced)',
    quantidade: 20
  },
  { _id: 'DOCUMENTARY FEATURE FILM', quantidade: 20 },
  { _id: 'MUSIC (Music Score of a Dramatic Picture)', quantidade: 20 },
  { _id: 'MUSIC (Original Musical or Comedy Score)', quantidade: 20 },
  { _id: 'DOCUMENTARY SHORT FILM', quantidade: 20 },
  { _id: 'MUSIC (Music Score--substantially original)', quantidade: 20 },
  { _id: 'WRITING (Adaptation)', quantidade: 17 },
  { _id: 'SPECIAL VISUAL EFFECTS', quantidade: 16 },
  { _id: 'SHORT SUBJECT (Comedy)', quantidade: 13 },
  { _id: 'SHORT SUBJECT (Novelty)', quantidade: 12 },
  { _id: 'WRITING', quantidade: 11 },
  {
    _id: 'WRITING (Screenplay Adapted from Other Material)',
    quantidade: 10
  },
  { _id: 'LIVE ACTION SHORT FILM', quantidade: 10 },
  { _id: 'MUSIC (Original Music Score)', quantidade: 10 },
  {
    _id: 'MUSIC (Score of a Musical Picture--original or adaptation)',
    quantidade: 10
  },
  {
    _id: 'WRITING (Screenplay Written Directly for the Screen--based on factual material or on story material not previously published or produced)',
    quantidade: 10
  },
  { _id: 'SOUND EFFECTS', quantidade: 10 },
  { _id: 'WRITING (ORIGINAL SCREENPLAY)', quantidade: 10 },
  { _id: 'MUSIC (ORIGINAL SONG)', quantidade: 10 },
  {
    _id: 'MUSIC (Original Score--for a motion picture [not a musical])',
    quantidade: 10
  },
  { _id: 'MUSIC (ORIGINAL SCORE)', quantidade: 10 },
  { _id: 'WRITING (ADAPTED SCREENPLAY)', quantidade: 10 },
  {
    _id: 'MUSIC (Scoring: Original Song Score and Adaptation -or- Scoring: Adaptation)',
    quantidade: 9
  },
  { _id: 'SHORT SUBJECT (Animated)', quantidade: 9 },
  { _id: 'SPECIAL ACHIEVEMENT AWARD (Visual Effects)', quantidade: 9 },
  { _id: 'MUSIC (Original Song Score)', quantidade: 8 },
  { _id: 'OUTSTANDING PICTURE', quantidade: 8 },
  {
    _id: 'MUSIC (Scoring: Adaptation and Original Song Score)',
    quantidade: 8
  },
  {
    _id: 'MUSIC (Original Song Score and Its Adaptation -or- Adaptation Score)',
    quantidade: 6
  },
  {
    _id: 'MUSIC (Original Song Score and Its Adaptation or Adaptation Score)',
    quantidade: 6
  },
  { _id: 'SHORT SUBJECT (Color)', quantidade: 6 },
  { _id: 'ANIMATED SHORT FILM', quantidade: 5 },
  { _id: 'WRITING (Screenplay--Original)', quantidade: 5 },
  {
    _id: 'WRITING (Story and Screenplay--based on material not previously published or produced)',
    quantidade: 5
  },
  { _id: 'WRITING (Screenplay--Adapted)', quantidade: 5 },
  { _id: 'CASTING', quantidade: 5 },
  { _id: 'HONORARY FOREIGN LANGUAGE FILM AWARD', quantidade: 5 },
  {
    _id: 'SPECIAL ACHIEVEMENT AWARD (Sound Effects Editing)',
    quantidade: 4
  },
  { _id: 'SHORT FILM (Dramatic Live Action)', quantidade: 3 },
  { _id: 'WRITING (Title Writing)', quantidade: 3 },
  { _id: 'SPECIAL ACHIEVEMENT AWARD', quantidade: 3 },
  { _id: 'UNIQUE AND ARTISTIC PICTURE', quantidade: 3 },
  { _id: 'MUSIC (Adaptation Score)', quantidade: 3 },
  { _id: 'ENGINEERING EFFECTS', quantidade: 3 },
  { _id: 'DIRECTING (Dramatic Picture)', quantidade: 3 },
  {
    _id: 'MUSIC (Original Song Score or Adaptation Score)',
    quantidade: 3
  },
  { _id: 'DIRECTING (Comedy Picture)', quantidade: 2 },
  { _id: 'SPECIAL FOREIGN LANGUAGE FILM AWARD', quantidade: 2 },
  { _id: 'SPECIAL ACHIEVEMENT AWARD (Sound Editing)', quantidade: 1 },
  { _id: 'SPECIAL ACHIEVEMENT AWARD (Sound Effects)', quantidade: 1 },
  { _id: 'GORDON E. SAWYER AWARD', quantidade: 1 },
  { _id: 'AWARD OF COMMENDATION', quantidade: 1 }
]
```

</details>
</details>
<br>

<details>
<summary><strong>🌟 2.2 Qual categoria teve mais indicações ao longo da história do Oscar?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.aggregate([
  { 
    $group: { 
      _id: "$categoria", 
      quantidade: { $sum: 1 } 
    } 
  },
  { 
    $sort: { quantidade: -1 }
  },
  {
    $limit: 1
  }
])
```

<details>
<summary><strong>Ver Resposta 🕵️‍♂️🔍</strong></summary>
<br>

```json
{
  _id: 'DIRECTING',
  quantidade: 479
}
```

</details>
</details>
<br>

<details>
<summary><strong>🎥 2.3 Qual categoria teve menos indicações ao longo da história?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.aggregate([
  { 
    $group: { 
      _id: "$categoria", 
      quantidade: { $sum: 1 } 
    } 
  },
  { 
    $sort: { quantidade: 1 }
  },
  {
    $limit: 1
  }
])
```

<details>
<summary><strong>Ver Resposta 🕵️‍♂️🔍</strong></summary>
<br>

```json
{
  _id: 'SPECIAL ACHIEVEMENT AWARD (Sound Effects)',
  quantidade: 1
}
```

</details>
</details>
<br>

<details>
<summary><strong> 🎞️ 2.4 A partir de que ano a categoria "ACTRESS" deixou de existir? (Dica: procure a última cerimônia com essa categoria)</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.aggregate([
    {
    $match: {
      categoria: 'ACTRESS'
    }
  },
  { 
    $group: { 
      _id: "$categoria", 
      ano_cerimonia: { $max: "$ano_cerimonia" }
    } 
  },
  {
    $limit: 1
  }
])
```

<details>
<summary><strong>Ver Resposta 🕵️‍♂️🔍</strong></summary>
<br>

```json
{
  _id: 'ACTRESS',
  ano_cerimonia: 1976
}
```

</details>
</details>
<br>

<details>
<summary><strong>🎞️ 2.5 Quais categorias existiam na primeira cerimônia (1928) e não existem mais hoje?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.distinct("categoria", {ano_cerimonia: 1928}).filter(categoria => !db.oscar.distinct("categoria", {ano_cerimonia: 2026}).includes(categoria));
```

<details>
<summary><strong>Ver Resposta 🕵️‍♂️🔍</strong></summary>
<br>

```json
[
  'ACTOR',
  'ACTRESS',
  'ART DIRECTION',
  'DIRECTING (Comedy Picture)',
  'DIRECTING (Dramatic Picture)',
  'ENGINEERING EFFECTS',
  'OUTSTANDING PICTURE',
  'SPECIAL AWARD',
  'UNIQUE AND ARTISTIC PICTURE',
  'WRITING (Adaptation)',
  'WRITING (Original Story)',
  'WRITING (Title Writing)'
]
```

</details>
</details>
<br>

<details>
<summary><strong>🎞️ 2.6 Liste todas as categorias que contêm a palavra "DIRECTING" no nome.</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.distinct("categoria").filter(categoria => categoria.includes("DIRECTING"))
```

<details>
<summary><strong>Ver Resposta 🕵️‍♂️🔍</strong></summary>
<br>

```json
[
  'DIRECTING',
  'DIRECTING (Comedy Picture)',
  'DIRECTING (Dramatic Picture)'
]
```

</details>
</details>
<br>
</details>

<details>
<summary><strong><h3 style="display: inline-block">📂 Nível 3: Atores e Atrizes Famosos</h3></strong></summary>
<br>

<details>
<summary><strong>🎭 3.1 Quantas vezes Natalie Portman foi indicada ao Oscar?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.countDocuments({nome_do_indicado: "Natalie Portman"})
```

<details>
<summary><strong>Ver Resposta 🕵️‍♂️🔍</strong></summary>
<br>

```json
R: 3 vezes
```

</details>
</details>
<br>

<details>
<summary><strong>🎭 3.2 Quantos Oscars Natalie Portman ganhou?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.countDocuments({nome_do_indicado: "Natalie Portman", vencedor: true})
```

<details>
<summary><strong>Ver Resposta 🕵️‍♂️🔍</strong></summary>
<br>

```json
R: 1 vez
```

</details>
</details>
<br>

