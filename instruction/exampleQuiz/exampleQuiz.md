# Example Quiz

This demonstrates how to write quizzes in Mastery LS format.

```masteryls
{"id":"8972e7ef-a15b-4973-a401-a8ad1637f06f", "title":"Multiple choice", "type":"multiple-choice", "body":"Simple **multiple choice** question" }
- [ ] This is **not** the right answer
- [x] This is _the_ right answer
- [ ] This one has a [link](https://cow.com)
- [ ] This one has an image ![Stock Photo](https://images.unsplash.com/photo-1506744038136-46273834b3fb?auto=format&fit=crop&w=400&q=80)
```

```masteryls
{"id":"e6db50da-1a13-4e86-bc42-2a946a003400", "title":"Multiple select", "type":"multiple-select", "body": "A **multiple select** question can have multiple answers. Incorrect selections count against correct ones when calculating the correct percentage." }
- [ ] This is **not** the right answer
- [x] This is _the_ right answer
- [ ] This is **not** the right answer
- [x] Another right answer
- [ ] This is **not** the right answer
```

```masteryls
{"id":"d63a8e3f-095a-4ef8-b685-bc71e6db03af", "title":"Essay", "type":"essay", "body":"Simple **essay** question" }
```

```masteryls
{"id":"3f343c83-02fa-4345-a858-08a26c9e3e76", "title":"File submission", "type":"file-submission", "body":"Simple **submission** by file", "allowComment":true  }
```

```masteryls
{"id":"44f7b4f3-4495-4c14-b1a7-6fe3011c51fe", "title":"URL submission", "type":"url-submission", "body":"Simple **submission** by url", "allowComment":true }
```
