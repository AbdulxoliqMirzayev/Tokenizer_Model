# Tokenizer_Model

# **O‘zbekcha Tokenizer Modeli (`uz_tokenizer-v2`)**

Bu loyiha **O‘zbek tili uchun yangi tokenizer modeli**ni yaratish va sinab ko‘rish uchun tayyorlangan. Ushbu hujjatda loyihani qanday ishlatish, modelni qanday o‘rgatish va foydalanish haqida ma'lumot berilgan.

---

## **Loyiha Maqsadi**

O‘zbek tilidagi matnlarni tokenlarga bo‘lish uchun yangi tokenizer yaratildi. Ushbu tokenizer o‘zbek tilidagi jumlalarni tahlil qilish va ularni mashinaga tushunarli formatga ajratish imkoniyatini beradi.

---

## **Foydalanilgan Kutubxonalar**

Loyihada quyidagi Python kutubxonalari ishlatilgan:
- `transformers`: Model va tokenizer yaratish uchun
- `datasets`: Ma'lumotlar to‘plamini yuklash uchun
- `huggingface_hub`: Hugging Face repozitoriyasiga yuklash uchun

---

## **Loyiha Bosqichlari**

### **1. Ma'lumotlarni Yuklash va Tahlil**
```python
from datasets import load_dataset

dataset = load_dataset("common_voice", "uz")
print(dataset)
```
**Ma'lumotlar haqida qisqacha ma'lumot:** `common_voice` datasetidan olingan ma'lumotlar yuklandi va o‘rganildi.

---

### **2. Eski Tokenizerdan Foydalanish**
Oldingi model sifatida `FacebookAI/xlm-roberta-base` ishlatildi:
```python
from transformers import AutoTokenizer

old_tokenizer = AutoTokenizer.from_pretrained("xlm-roberta-base")
```

---

### **3. Yangi Tokenizerni Yaratish**
Yangi tokenizerni tayyorlash uchun matn to‘plamidan foydalanildi:
```python
new_tokenizer = old_tokenizer.train_new_from_iterator(corpus, 120000)
new_tokenizer.save_pretrained("uz_tokenizer-v2")
```

---

### **4. Hugging Face Repozitoriyasiga Yuklash**
Hugging Face repozitoriyasiga yangi tokenizer yuklandi:
```python
from huggingface_hub import HfApi

api = HfApi()
api.upload_folder(folder_path="/content/uz_tokenizer-v2", repo_id="AbdulxoliqMirzaev/uz_tokenizer-v2", repo_type="model")
```

---

## **Modelni Yuklab Olish va Ishlatish**

Yangi tokenizerdan foydalanish uchun quyidagi kodni ishga tushiring:
```python
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained("AbdulxoliqMirzaev/uz_tokenizer-v2")
text = "Bu loyiha o‘zbek tilidagi matnlarni tokenlarga bo‘lish uchun!"
print(tokenizer.tokenize(text))
```

---

## **Natija**

Yangi tokenizer avvalgi tokenizerga nisbatan o‘zbek tilidagi matnlarni yaxshiroq segmentatsiya qiladi:
- **Eski tokenizer:** ['○bu', '○loyi', 'ha', ...]
- **Yangi tokenizer:** ['○Bu', '○loyiha', ...]

---

## **Loyiha Maqsadlari Kelgusi Bosqichlarda:**
- Dataset hajmini oshirish.
- O‘zbek tili uchun ko‘proq so‘z formalarini qo‘shish.
- Modelni boshqa loyihalarda integratsiya qilish.

---

### **Muallif**
Loyiha muallifi: **Abdulxoliq Mirzayev**  
Loyiha Hugging Face platformasida: [Havola](https://huggingface.co/AbdulxoliqMirzaev/uz_tokenizer-v2)


