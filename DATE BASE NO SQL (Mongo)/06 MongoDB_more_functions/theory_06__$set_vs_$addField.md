В MongoDB операторы `$set` и `$addFields` очень похожи.    
Оба используются для добавления новых полей или изменения существующих:

### 📌 Краткое различие:

| Оператор     | Где используется                   | Назначение                       |
| ------------ | ---------------------------------- | -------------------------------- |
| `$set`       | В **`update`** и **`aggregation`** | Устанавливает значение поля      |
| `$addFields` | Только в **`aggregation`**         | Добавляет новые поля в документы |

---

## 💡 В агрегатных пайплайнах (`$set` vs `$addFields`)

Они **идентичны по функциональности**.

Пример — это одно и то же:

```js
db.collection.aggregate([
  { $addFields: { fullName: { $concat: ["$firstName", " ", "$lastName"] } } }
])
```

```js
db.collection.aggregate([
  { $set: { fullName: { $concat: ["$firstName", " ", "$lastName"] } } }
])
```

**Разница** здесь чисто **семантическая**:

* `$addFields` — подчеркивает, что вы **добавляете** новое поле.
* `$set` — может как **добавить новое**, так и **изменить существующее**.

---

## ДОПОЛНИТЕЛЬНО: `$set` используется в `update`-операциях

* **`$set`** используется в операциях обновления документов (не в агрегации):

```js
db.collection.updateOne(
  { _id: 1 },
  { $set: { status: "active" } }
)
```

