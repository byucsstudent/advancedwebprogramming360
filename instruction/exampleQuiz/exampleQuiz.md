# Example Quiz

This demonstrates how to write quizzes in Mastery LS format.

```masteryls
{"id":"39280", "title":"Multiple choice", "type":"multiple-choice", "body":"Simple **multiple choice** question" }
- [ ] This is **not** the right answer
- [x] This is _the_ right answer
- [ ] This one has a [link](https://cow.com)
- [ ] This one has an image ![Stock Photo](https://images.unsplash.com/photo-1506744038136-46273834b3fb?auto=format&fit=crop&w=400&q=80)
```

```masteryls
{"id":"39281", "title":"Multiple select", "type":"multiple-select", "body": "A **multiple select** question can have multiple answers. Incorrect selections count against correct ones when calculating the correct percentage." }
- [ ] This is **not** the right answer
- [x] This is _the_ right answer
- [ ] This is **not** the right answer
- [x] Another right answer
- [ ] This is **not** the right answer
```

```masteryls
{"id":"39282", "title":"Essay", "type":"essay", "body":"Simple **essay** question" }
```

```masteryls
{"id":"39283", "title":"File submission", "type":"file-submission", "body":"Simple **submission** by file", "allowComment":true  }
```

```masteryls
{"id":"39284", "title":"URL submission", "type":"url-submission", "body":"Simple **submission** by url", "allowComment":true }
```
