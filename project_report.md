# تقرير مفصل لمشروع تطبيق توصيل الطعام في سوريا

## 1. البنية الكاملة للمشروع

### نظرة عامة على البنية
مشروع تطبيق توصيل الطعام في سوريا هو تطبيق ويب كامل (Full Stack) يتكون من ثلاثة أجزاء رئيسية:

1. **الواجهة الأمامية (Frontend)**: مبنية باستخدام React و TypeScript، مع دعم كامل للغة العربية واتجاه RTL.
2. **الخلفية (Backend)**: مبنية باستخدام Node.js و Express، مع دعم للمصادقة والتفويض.
3. **قاعدة البيانات**: PostgreSQL (عبر Supabase) مع استخدام Drizzle ORM للتعامل مع قاعدة البيانات.

### تدفق البيانات
1. **من المستخدم إلى الواجهة الأمامية**: يتفاعل المستخدم مع واجهة المستخدم المبنية بـ React.
2. **من الواجهة الأمامية إلى الخلفية**: تقوم الواجهة الأمامية بإرسال طلبات HTTP إلى الخلفية عبر API.
3. **من الخلفية إلى قاعدة البيانات**: تتعامل الخلفية مع قاعدة البيانات باستخدام Drizzle ORM.
4. **تحديثات في الوقت الحقيقي**: يستخدم التطبيق WebSocket للتحديثات في الوقت الحقيقي مثل تتبع الطلبات وإشعارات المطاعم.

### تفاعل المكونات الرئيسية
- **نظام المصادقة**: يستخدم Passport.js للمصادقة المحلية، مع دعم لـ Supabase Auth.
- **نظام السلة**: يستخدم Context API في React لإدارة سلة التسوق.
- **نظام تتبع الطلبات**: يستخدم WebSocket للتحديثات في الوقت الحقيقي.
- **نظام الإشعارات**: يستخدم Toast من shadcn/ui لعرض الإشعارات.
- **نظام التوجيه**: يستخدم مكتبة Wouter للتوجيه في الواجهة الأمامية.

## 2. مجموعة التقنيات المستخدمة

### الواجهة الأمامية (Frontend)
- **React**: إطار عمل JavaScript لبناء واجهات المستخدم.
- **TypeScript**: لغة برمجة تضيف أنواع ثابتة إلى JavaScript.
- **Tailwind CSS**: إطار عمل CSS للتصميم السريع.
- **shadcn/ui**: مكتبة مكونات واجهة المستخدم المبنية على Radix UI.
- **Framer Motion**: مكتبة للرسوم المتحركة.
- **React Query**: لإدارة حالة البيانات وطلبات الشبكة.
- **Wouter**: مكتبة توجيه خفيفة الوزن لـ React.
- **Zod**: مكتبة للتحقق من صحة البيانات.
- **React Hook Form**: لإدارة النماذج.

### الخلفية (Backend)
- **Node.js**: بيئة تشغيل JavaScript على الخادم.
- **Express**: إطار عمل لبناء تطبيقات الويب.
- **WebSocket (ws)**: لاتصالات ثنائية الاتجاه في الوقت الحقيقي.
- **Passport.js**: لإدارة المصادقة.
- **bcrypt**: لتشفير كلمات المرور.
- **express-session**: لإدارة جلسات المستخدم.

### قاعدة البيانات
- **PostgreSQL**: نظام إدارة قواعد البيانات العلائقية.
- **Supabase**: منصة Backend-as-a-Service تستخدم PostgreSQL.
- **Drizzle ORM**: مكتبة ORM للتعامل مع قاعدة البيانات.
- **Drizzle Kit**: أدوات لإدارة مخططات قاعدة البيانات والترحيلات.

### أدوات التطوير
- **Vite**: أداة بناء وتطوير سريعة.
- **ESBuild**: مجمع JavaScript سريع.
- **TypeScript**: للتحقق من الأنواع.
- **Tailwind CSS**: لتصميم واجهة المستخدم.

## 3. تحليل هيكل الملفات

### الهيكل العام للمشروع
```
SyriaFoodApp/
├── client/                 # كود الواجهة الأمامية
│   ├── src/
│   │   ├── components/     # مكونات React
│   │   ├── context/        # سياقات React
│   │   ├── hooks/          # هوكات React المخصصة
│   │   ├── lib/            # مكتبات وأدوات مساعدة
│   │   ├── pages/          # صفحات التطبيق
│   │   ├── styles/         # ملفات CSS
│   │   ├── utils/          # وظائف مساعدة
│   │   ├── App.tsx         # المكون الرئيسي للتطبيق
│   │   └── main.tsx        # نقطة الدخول للتطبيق
├── server/                 # كود الخلفية
│   ├── middleware/         # وسائط Express
│   ├── routes/             # مسارات API
│   ├── auth.ts             # إدارة المصادقة
│   ├── db.ts               # اتصال قاعدة البيانات
│   ├── index.ts            # نقطة الدخول للخادم
│   ├── routes.ts           # تسجيل المسارات
│   ├── seed.js             # بيانات أولية
│   ├── storage.ts          # واجهة التخزين
│   ├── supabase.ts         # إعداد Supabase
│   └── vite.ts             # إعداد Vite للتطوير
└── shared/                 # كود مشترك بين الواجهة الأمامية والخلفية
    ├── payment.ts          # نظام الدفع
    ├── schema.ts           # مخطط قاعدة البيانات
    ├── types.ts            # أنواع TypeScript المشتركة
    └── validations.ts      # التحقق من صحة البيانات
```

### الملفات الرئيسية وأهميتها

#### الواجهة الأمامية (Frontend)
- **client/src/App.tsx**: المكون الرئيسي للتطبيق، يحدد مسارات التطبيق وهيكل الصفحة.
- **client/src/context/AuthContext.tsx**: يدير حالة المصادقة في التطبيق.
- **client/src/context/CartContext.tsx**: يدير سلة التسوق.
- **client/src/context/WebSocketContext.tsx**: يدير اتصالات WebSocket للتحديثات في الوقت الحقيقي.
- **client/src/hooks/useOrderTracking.ts**: هوك لتتبع حالة الطلب في الوقت الحقيقي.
- **client/src/components/OrderTracker.tsx**: مكون لعرض حالة الطلب وتتبعه.
- **client/src/pages/restaurant/DashboardPage.tsx**: لوحة تحكم لأصحاب المطاعم.
- **client/src/pages/delivery/DashboardPage.tsx**: لوحة تحكم لعمال التوصيل.

#### الخلفية (Backend)
- **server/index.ts**: نقطة الدخول للخادم، يقوم بإعداد Express وتسجيل المسارات.
- **server/routes.ts**: يحدد مسارات API ويعد خادم WebSocket.
- **server/auth.ts**: يدير المصادقة والتفويض.
- **server/storage.ts**: واجهة للتعامل مع قاعدة البيانات.
- **server/seed.js**: يقوم بتعبئة قاعدة البيانات بالبيانات الأولية.

#### المشترك (Shared)
- **shared/schema.ts**: يحدد مخطط قاعدة البيانات باستخدام Drizzle ORM.
- **shared/payment.ts**: يحدد طرق الدفع المدعومة ومخططات التحقق.
- **shared/validations.ts**: يحدد مخططات التحقق من صحة البيانات.

## 4. شرح مخطط قاعدة البيانات

### الجداول الرئيسية

#### جدول المستخدمين (users)
- يخزن معلومات المستخدمين بما في ذلك الاسم، البريد الإلكتروني، كلمة المرور، الدور.
- الأدوار المدعومة: عميل، مطعم، عامل توصيل، مدير.

#### جدول العناوين (addresses)
- يخزن عناوين المستخدمين مع إحداثيات الموقع.
- مرتبط بجدول المستخدمين بعلاقة متعددة (many-to-one).

#### جدول المطاعم (restaurants)
- يخزن معلومات المطاعم بما في ذلك الاسم، الوصف، العنوان، الموقع، نوع المطبخ.
- يتضمن معلومات إضافية مثل التقييم، الحد الأدنى للطلب، رسوم التوصيل.

#### جدول الفئات (categories)
- يخزن فئات الطعام مثل شاورما، بيتزا، برغر، مشاوي.

#### جدول عناصر القائمة (menu_items)
- يخزن عناصر القائمة لكل مطعم.
- مرتبط بجدول المطاعم وجدول الفئات.

#### جدول الطلبات (orders)
- يخزن معلومات الطلبات بما في ذلك المستخدم، المطعم، العنوان، الحالة، المجموع.
- حالات الطلب: معلق، مقبول، قيد التحضير، جاهز للاستلام، قيد التوصيل، تم التوصيل، ملغي.

#### جدول عناصر الطلب (order_items)
- يخزن عناصر كل طلب مع الكمية والسعر.
- مرتبط بجدول الطلبات وجدول عناصر القائمة.

#### جدول عمال التوصيل (delivery_persons)
- يخزن معلومات عمال التوصيل بما في ذلك الموقع الحالي وحالة التوفر.
- مرتبط بجدول المستخدمين.

#### جدول التوصيلات (deliveries)
- يخزن معلومات التوصيل بما في ذلك الطلب، عامل التوصيل، الحالة، الأوقات.
- حالات التوصيل: معين، تم الاستلام، تم التوصيل، فشل التوصيل.

#### جدول العروض الترويجية (promotions)
- يخزن معلومات العروض الترويجية مثل الرمز، العنوان، نوع الخصم، القيمة.

### العلاقات بين الجداول
- **المستخدمين والعناوين**: علاقة واحد إلى متعدد (one-to-many).
- **المستخدمين والطلبات**: علاقة واحد إلى متعدد.
- **المطاعم وعناصر القائمة**: علاقة واحد إلى متعدد.
- **المطاعم والطلبات**: علاقة واحد إلى متعدد.
- **الفئات وعناصر القائمة**: علاقة واحد إلى متعدد.
- **الطلبات وعناصر الطلب**: علاقة واحد إلى متعدد.
- **عمال التوصيل والتوصيلات**: علاقة واحد إلى متعدد.

### استخدام Drizzle ORM
- يستخدم المشروع Drizzle ORM للتعامل مع قاعدة البيانات.
- يتم تعريف مخطط قاعدة البيانات في ملف `shared/schema.ts`.
- يتم استخدام Drizzle Zod لإنشاء مخططات التحقق من صحة البيانات.
- يتم استخدام Drizzle Kit لإدارة ترحيلات قاعدة البيانات.

## 5. حالة تنفيذ الميزات الحالية

### الميزات المنفذة

#### المصادقة والتفويض
- ✅ تسجيل الدخول وتسجيل الخروج
- ✅ تسجيل المستخدمين الجدد
- ✅ التحقق من الدور والصلاحيات
- ✅ حماية المسارات بناءً على الدور

#### واجهة المستخدم العامة
- ✅ الصفحة الرئيسية
- ✅ صفحة المطاعم
- ✅ صفحة تفاصيل المطعم
- ✅ صفحة الفئات
- ✅ صفحة المطاعم الشائعة
- ✅ صفحة الأطباق الشائعة

#### سلة التسوق والدفع
- ✅ إضافة العناصر إلى السلة
- ✅ تعديل الكمية في السلة
- ✅ إزالة العناصر من السلة
- ✅ صفحة الدفع
- ✅ نظام الدفع المناسب للسوق السورية

#### تتبع الطلبات
- ✅ تتبع حالة الطلب في الوقت الحقيقي
- ✅ عرض موقع عامل التوصيل على الخريطة
- ✅ تحديثات حالة الطلب

#### واجهة صاحب المطعم
- ✅ لوحة تحكم المطعم
- ✅ إدارة الطلبات (قبول/رفض، تحديث الحالة)
- ✅ تلقي إشعارات الطلبات الجديدة

#### واجهة عامل التوصيل
- ✅ لوحة تحكم عامل التوصيل
- ✅ عرض الطلبات المسندة
- ✅ تحديث حالة التوصيل
- ✅ إرسال تحديثات الموقع

#### واجهة المدير
- ✅ لوحة تحكم المدير
- ✅ إدارة المستخدمين
- ✅ إدارة المطاعم
- ✅ إدارة الطلبات
- ✅ إدارة عمال التوصيل
- ✅ التقارير والإحصائيات

### الميزات المفقودة أو غير المكتملة

#### المصادقة والتفويض
- ❌ استعادة كلمة المرور
- ❌ المصادقة الثنائية
- ❌ تسجيل الدخول باستخدام وسائل التواصل الاجتماعي

#### واجهة المستخدم العامة
- ❌ البحث المتقدم
- ❌ التصفية حسب المسافة
- ❌ التصفية حسب وقت التوصيل

#### سلة التسوق والدفع
- ❌ تكامل بوابات الدفع الإلكتروني
- ❌ حفظ طرق الدفع المفضلة
- ❌ تطبيق الكوبونات والعروض الترويجية

#### تتبع الطلبات
- ❌ تقدير وقت الوصول
- ❌ الاتصال المباشر بعامل التوصيل
- ❌ تقييم التوصيل

#### واجهة صاحب المطعم
- ❌ إدارة القائمة (إضافة/تعديل/حذف العناصر)
- ❌ إدارة ساعات العمل
- ❌ إدارة العروض الترويجية
- ❌ التقارير والإحصائيات

#### واجهة عامل التوصيل
- ❌ جدولة أوقات العمل
- ❌ حساب المكافآت والعمولات
- ❌ تاريخ التوصيلات

#### واجهة المدير
- ❌ إدارة العروض الترويجية
- ❌ إدارة الفئات
- ❌ إعدادات النظام

## 6. التحديات والمشكلات المحتملة

### تحديات تقنية
1. **دعم RTL**: ضمان دعم كامل لاتجاه RTL في جميع أجزاء التطبيق.
2. **أداء WebSocket**: ضمان استقرار اتصالات WebSocket للتحديثات في الوقت الحقيقي.
3. **تكامل خرائط Google**: تنفيذ تتبع الموقع وعرض المسار بشكل صحيح.
4. **التجاوب مع الأجهزة المحمولة**: ضمان عمل التطبيق بشكل جيد على مختلف أحجام الشاشات.

### تحديات الأعمال
1. **خصوصية السوق السورية**: تكييف التطبيق مع احتياجات السوق السورية.
2. **طرق الدفع**: دعم طرق الدفع المناسبة للسوق السورية.
3. **تجربة المستخدم**: تحسين تجربة المستخدم لتكون سلسة وبديهية.
4. **الأمان**: ضمان أمان البيانات والمعاملات.

## 7. الخلاصة

مشروع تطبيق توصيل الطعام في سوريا هو تطبيق ويب كامل مبني باستخدام تقنيات حديثة مثل React، TypeScript، Node.js، Express، PostgreSQL، وWebSocket. يوفر التطبيق واجهات مستخدم مختلفة للعملاء، أصحاب المطاعم، عمال التوصيل، والمديرين، مع دعم كامل للغة العربية واتجاه RTL.

المشروع يتضمن العديد من الميزات المنفذة مثل المصادقة، سلة التسوق، تتبع الطلبات، وإدارة الطلبات، ولكن هناك بعض الميزات المفقودة أو غير المكتملة مثل استعادة كلمة المرور، البحث المتقدم، وتكامل بوابات الدفع الإلكتروني.

التحديات الرئيسية تشمل ضمان دعم كامل لاتجاه RTL، استقرار اتصالات WebSocket، تكامل خرائط Google، والتجاوب مع الأجهزة المحمولة، بالإضافة إلى تكييف التطبيق مع احتياجات السوق السورية ودعم طرق الدفع المناسبة.
