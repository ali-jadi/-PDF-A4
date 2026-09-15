# -PDF-A4
pdf-resizer-tool
# PDF Page Resizer (أداة تعديل مقاسات ملفات الـ PDF)

أداة بسيطة وفعالة بلغة بايثون (Python) لتعديل أبعاد صفحات ملفات الـ PDF وتحويلها تلقائياً إلى مقاس **A4** بالوضع الأفقي (Landscape) أو القياسي، باستخدام مكتبة `pypdf`.

---

## 🚀 المميزات
* **تعديل تلقائي:** يقوم بقراءة أبعاد جميع صفحات ملف الـ PDF الأصلي وحساب نسب التمدد والتصغير بدقة.
* **الحفاظ على المحتوى:** يعيد تحجيم كل صفحة وتطبيق الـ Transformations المناسبة لتلائم مقاس A4 تماماً.
* **خفيف وسريع:** يعتمد على مكتبة `pypdf` الحديثة والسريعة في معالجة الملفات.

---

## 📦 المتطلبات والمكتبات المستخدمة
تحتاج لتثبيت مكتبة `pypdf` قبل تشغيل الكود. يمكنك تثبيتها بسهولة عبر الأمر التالي في الطرفية (Terminal) أو داخل Google Colab:

```bash
pip install pypdf
💻 طريقة الاستخدام
تأكد من وضع ملف الـ PDF المراد تعديله في نفس مجلد العمل (أو قم بتحديد مسار الملف كاملاً).

افتح الكود وشغله (سواء عبر Google Colab أو بيئة عمل بايثون المحلية).

سيقوم الكود بمعالجة الصفحات وإخراج ملف جديد باسم output_A4.pdf.
from pypdf import PdfReader, PdfWriter, Transformation

# قراءة الملف الأصلي
reader = PdfReader("الجزء 1 من كتاب حروفي الجميلة 8-9-2026.pdf")
writer = PdfWriter()

# تحديد أبعاد مقاس A4 أفقي (Landscape)
a4_width = 841.89
a4_height = 595.28

for page in reader.pages:
    current_width = float(page.mediabox.width)
    current_height = float(page.mediabox.height)

    # حساب نسبة التغيير للعرض والطول
    scale_x = a4_width / current_width
    scale_y = a4_height / current_height

    # تطبيق التعديل والأبعاد الجديدة على الصفحة
    page.add_transformation(Transformation().scale(sx=scale_x, sy=scale_y))
    page.mediabox.upper_right = (a4_width, a4_height)
    page.cropbox.upper_right = (a4_width, a4_height)

    writer.add_page(page)

# حفظ الملف الناتج
with open("output_A4.pdf", "wb") as f:
    writer.write(f)

print("تم تحويل الملف بنجاح تام!")
📌 ملاحظات
إذا كنت ترغب في تحويل الملف إلى مقاس A4 رأسي (Portrait)، يمكنك عكس قيم الأبعاد بحيث تصبح a4_width = 595.28 و a4_height = 841.89.
