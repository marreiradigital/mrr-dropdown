Aqui está um `README.md` pronto para você publicar no GitHub do **MRR Dropdown**:

````markdown
# MRR Dropdown

Componente de **dropdown customizado** em Vanilla JS, sem dependências externas.  
Ele converte automaticamente qualquer `<select class="mrr-dropdown">` em um dropdown com:

- Suporte a **single** e **múltipla seleção**
- **Busca integrada** (opcional, acento-insensível, com highlight)
- Suporte a **`<optgroup>`**
- Animações de abertura/fechamento
- API pública em JavaScript
- Evento custom `mrr:change`

---

## 🚀 Instalação

Inclua o CSS:

```html
<link rel="stylesheet" href="/path/style.css">
ou https://cdn.jsdelivr.net/gh/marreiradigital/mrr-dropdown@main/style-min.css
````

Inclua o JS:

```html
<script src="/path/mrr-dropdown.js"></script>
ou
https://cdn.jsdelivr.net/gh/marreiradigital/mrr-dropdown@main/mrr-dropdown-min.js
```

O script inicializa automaticamente no `DOMContentLoaded`, convertendo todos os `select.mrr-dropdown`.
Se você inserir selects via AJAX/SPA, chame manualmente:

```js
initMrrDropdownsFromSelects();
```

---

## 📄 Exemplos de uso

### Single

```html
<select name="order" id="order" class="mrr-dropdown" data-placeholder="Selecione">
  <option value="">Selecione</option>
  <option value="relevancia">Relevância</option>
  <option value="avaliacao">Melhor avaliação</option>
</select>
```

### Múltiplo

```html
<select name="filtros[]" class="mrr-dropdown" multiple data-placeholder="Selecione filtros">
  <option value="a">A</option>
  <option value="b">B</option>
  <option value="c">C</option>
</select>
```

### Com `<optgroup>`

```html
<select class="mrr-dropdown" data-placeholder="Selecione">
  <option value="">Selecione</option>
  <optgroup label="Relevância">
    <option value="relevancia">Relevância</option>
    <option value="avaliacao">Melhor avaliação</option>
  </optgroup>
  <optgroup label="Localização" disabled>
    <option value="distancia">Distância</option>
  </optgroup>
</select>
```

---

## 🔍 Busca

Ative de duas formas:

```html
<select class="mrr-dropdown" search data-search-placeholder="Filtrar..." data-search-name="busca_order">
  ...
</select>
```

* `search` → ativa busca
* `data-search-placeholder="..."` → placeholder custom
* `data-search-name="..."` → name do input

---

## 🎨 Classes úteis

* **Container**: `.mrr-dropdown` (+ `.is-disabled`)
* **Cabeçalho**: `.mrr-input` → `.valor-selected` + `.icon-down`
* **Lista**: `.mrr-content-dropdown` → `.item` (+ `.ativo`, `.is-hidden`)
* **Busca**: `.mrr-search` + `.mrr-search-input`, highlight com `.mrr-hl`
* **Grupos**: `.mrr-group`, `.mrr-group-label`, `.mrr-group-items`

O CSS já traz:

* Largura auto-ajustável (`min-width: max-content`)
* Marca visual ✓ no item selecionado
* Estilo para optgroups

---

## 📦 API Pública

```js
// Selecionar programaticamente
mrr_selected_dropdown('order', 'avaliacao');       // single
mrr_selected_dropdown('filtros', ['a','c']);       // múltiplo

// Renderizar itens dinamicamente
mrr_render_itens('filtros', [
  { label:'Grupo 1', items:[{value:'a',label:'A'},{value:'b',label:'B'}] },
  { value:'c', label:'Fora do grupo' }
]);

// Ler seleção
mrr_get_selected_values('filtros'); // ["a","c"]
mrr_get_selected_labels('filtros'); // ["A","C"]

// Controle de UI
mrr_open_dropdown('order');
mrr_close_dropdown('order');
mrr_toggle_dropdown('order');
mrr_clear_dropdown('filtros');
```

---

## 📡 Evento `mrr:change`

Disparado em qualquer mudança (clique ou API):

```js
document.addEventListener('mrr:change', (e) => {
  const { dataId, multiple, labels, values } = e.detail;
  if (dataId === 'filtros') {
    document.querySelector('#filtros_hidden').value = values.join(',');
  }
});
```

---

## 🛠️ Integração com formulários (WordPress/PHP)

O `<select>` original permanece no DOM (visualmente oculto) e submete normalmente.
Se preferir, capture o evento `mrr:change` e grave em um campo `hidden`.

---

## ⚠️ Troubleshooting

* **“Só aparece (+N)” no múltiplo**: abra o dropdown antes de setar valores em modais (largura depende do elemento visível).
* **Busca não encontra com acentos**: esperado, pois a normalização remove acentos.

---

## 📜 Licença

MIT © 2025 — Desenvolvido por \[Marreira]
