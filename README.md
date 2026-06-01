# Projeto Grupo 3
Naiely | Kelly* | Gustavo*

---

## 📋 Avaliação do Código HTML

### ✅ Pontos Positivos

1. **Tags semânticas bem utilizadas**: `<header>`, `<main>`, `<section>`, `<aside>` e `<footer>` estão corretamente posicionadas
2. **Sem div soup**: Não há uso excessivo de divs desnecessárias
3. **Estrutura geral apropriada**: Layout semântico claro

---

### ❌ Erros Críticos

#### 1. **Estrutura da Tabela (ERRO GRAVE)**

**Problemas identificados:**
- `</table>` está **antes** de `<thead>` (ordem errada)
- `<thead>` fica **fora** da tabela
- Mistura `<th>` com `<td>` incorretamente
- `<thead>` vem **após** `<tbody>` (ordem invertida)

**Correção necessária:**
```html
<table>
    <thead>
        <tr>
            <th>Dias</th>
            <th>Horários</th>
            <th>Turma</th>
            <th>Professores</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Segunda</td>
            <td>08:00</td>
            <td>1º A</td>
            <td>Professor X</td>
        </tr>
    </tbody>
</table>
```

---

#### 2. **Formulário Incompleto (ERRO MÉDIO)**

**Problemas identificados:**
- `<selection>` não existe em HTML5 (deveria ser `<select>`)
- `<select>` está **fora** do `<form>`
- `<button>` está **fora** do `<form>`
- Atributos vazios: `action=""`, `name=""`, `id=""`, `type=""`
- `<label>` não está associada (falta `for` correto)

**Correção necessária:**
```html
<form action="/reserva" method="POST">
    <label for="professor">Nome do Professor</label>
    <input type="text" name="professor" id="professor" required>

    <label for="data">Data</label>
    <input type="date" name="data" id="data" required>

    <label for="horario">Horário</label>
    <input type="time" name="horario" id="horario" required>

    <label for="projetor">Equipamento</label>
    <select name="projetor" id="projetor" required>
        <option value="">Selecione um equipamento</option>
        <option value="projetor1">Projetor 1</option>
        <option value="projetor2">Projetor 2</option>
        <option value="tv">TV</option>
    </select>

    <button type="submit">Reservar</button>
</form>
```

---

#### 3. **Indentação Inconsistente (ERRO LEVE)**

- Alguns elementos têm indentação irregular
- Não segue padrão consistente (2 ou 4 espaços)
- Faltam quebras de linha em lugares apropriados

---

### 📊 Resumo da Avaliação

| Critério | Status | Observações |
|----------|--------|------------|
| **Tags Semânticas** | ✅ Bom | Header, main, section, aside, footer corretos |
| **Estrutura de Tabela** | ❌ Crítico | Ordem errada, tags fora do lugar |
| **Formulários** | ❌ Crítico | `<selection>` errado, elementos fora do form |
| **Associação Label-Input** | ⚠️ Incompleto | Labels sem `for` correto |
| **Indentação e Limpeza** | ⚠️ Regular | Inconsistente, precisa padronizar |

**Nota estimada: 3/10** (com erros) + Ponto_Extra 5 = 8.0

---

### 📎 Referências
- [index.html](https://github.com/FranciscoDias87/prova-projetores-grupo3/blob/master/index.html)

# Avaliação do app.js: 5/10 = Ponto+Extra 5 = 10

## Resumo
O código mostra compreensão básica de conceitos JavaScript, mas tem problemas críticos de lógica e estrutura que impediriam o funcionamento correto em produção.

---

## ✅ Pontos Positivos

1. **Validação de campos** - Tenta validar se os campos estão preenchidos
2. **Validação de data** - Verifica se a data não é no passado
3. **Uso de localStorage** - Tenta persistir dados (conceito avançado para iniciante)
4. **Manipulação do DOM** - Cria linhas de tabela dinamicamente
5. **Estrutura legível** - Código organizado e fácil de ler

---

## ❌ Problemas Críticos

### 1. **Variável `reservationForm` declarada duas vezes**
```javascript
const reservationForm = document.querySelector('#reservation-form');
const reservationForm = document.querySelector('#reservation-form'); // ❌ Duplicado
```
**Solução:** Remover a linha duplicada.

---

### 2. **Lógica fora do evento `submit`**
O código que valida e processa o formulário está **fora** do `addEventListener`. Ele executa assim que a página carrega, não quando o usuário submete!

```javascript
reservationForm.addEventListener('submit', function(event) {
    event.preventDefault();
    console.log('Formulário enviado');
});
// ❌ Todo o resto do código deveria estar DENTRO do addEventListener!
const teacherName = document.querySelector('#teacher-name').value;
```

**Solução:** Mover todo o código de validação e processamento para **dentro** do evento submit.

---

### 3. **Variável `contactInfo` não definida**
```javascript
contactInfo  // ❌ Não existe!
```
Está sendo usada mas nunca foi capturada do formulário.

---

### 4. **Banco de dados reiniciado a cada carregamento**
```javascript
const reservationDatabase = [];  // ❌ Sempre vazio!
```
O array começa vazio e nunca carrega os dados salvos no localStorage. Deveria ser:
```javascript
const reservationDatabase = JSON.parse(localStorage.getItem('reservations')) || [];
```

---

### 5. **Validação de campos incorreta**
```javascript
if (teacherName === ' ' || ...) // ❌ Verifica espaço, não string vazia
```
Deveria ser:
```javascript
if (teacherName === '' || teacherName.trim() === '') // ✅ Correto
```

---

### 6. **Verificação de conflito sem efeito**
```javascript
const isReserved = reservationDatabase.some(...);
// O código calcula mas NUNCA usa essa variável! ❌
```

---

### 7. **Variável `reservationList` não definida**
```javascript
reservationList.appendChild(tableRow);  // ❌ De onde vem isso?
```

---

## 📋 Código Corrigido (Estrutura)

```javascript
const reservationForm = document.querySelector('#reservation-form');
const reservationList = document.querySelector('#reservationList'); // ✅ Adicionar

let reservationDatabase = JSON.parse(localStorage.getItem('reservations')) || []; // ✅ Carregar dados

reservationForm.addEventListener('submit', function(event) {
    event.preventDefault();
    
    // ✅ Capturar dados DENTRO do evento
    const teacherName = document.querySelector('#teacher-name').value.trim();
    const reservationDate = document.querySelector('#reservationDate').value;
    const startTime = document.querySelector('#startTime').value;
    const projectorModel = document.querySelector('#projectorModel').value;
    const contactInfo = document.querySelector('#contactInfo').value.trim(); // ✅ Faltava!
    
    // ✅ Validações
    if (!teacherName || !reservationDate || !startTime || !projectorModel || !contactInfo) {
        alert('Preencha todos os campos!');
        return;
    }
    
    const currentDate = new Date().toISOString().split('T')[0];
    if (reservationDate < currentDate) {
        alert('Não é permitido agendar datas passadas!');
        return;
    }
    
    // ✅ Verificar conflito
    const isReserved = reservationDatabase.some(reservation =>
        reservation.projectorModel === projectorModel &&
        reservation.reservationDate === reservationDate &&
        reservation.startTime === startTime
    );
    
    if (isReserved) {
        alert('Este projetor já está reservado nessa data/hora!');
        return;
    }
    
    // ✅ Adicionar à base de dados
    const newReservation = { teacherName, reservationDate, startTime, projectorModel, contactInfo };
    reservationDatabase.push(newReservation);
    
    // ✅ Atualizar localStorage
    localStorage.setItem('reservations', JSON.stringify(reservationDatabase));
    
    // ✅ Adicionar à tabela
    const tableRow = document.createElement('tr');
    tableRow.innerHTML = `
        <td>${teacherName}</td>
        <td>${reservationDate}</td>
        <td>${startTime}</td>
        <td>${projectorModel}</td>
        <td>${contactInfo}</td>
    `;
    reservationList.appendChild(tableRow);
    
    // ✅ Limpar formulário
    reservationForm.reset();
    console.log('Reserva criada com sucesso!');
});
```

---

## 🎯 Recomendações para Aprender

1. **Entenda escopos** - Diferença entre código fora e dentro de funções
2. **Use o console** - `console.log()` para debugar valores
3. **Valide sempre** - Verifique se variáveis existem antes de usar
4. **Organize melhor** - Separar captura de dados, validação e processamento
5. **Teste incrementalmente** - Escreva pouco código e teste logo

---

**Nota:** Para um aluno iniciante, é um código com uma boa ideia geral, mas precisa de ajustes importantes para funcionar corretamente!
