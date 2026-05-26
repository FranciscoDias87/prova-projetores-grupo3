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

**Nota estimada: 5-6/10** (com erros) → **8-9/10** (após correções)

---

### 📎 Referências
- [index.html](https://github.com/FranciscoDias87/prova-projetores-grupo3/blob/master/index.html)
