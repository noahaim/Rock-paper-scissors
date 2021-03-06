# אבן נייר ומספריים:
**נועה חיים&יערה ברק**

![](https://github.com/noahaim/Rock-paper-scissors/blob/8279b10dceb399d604562f477734a8ed48b150c0/WhatsApp%20Image%202022-02-11%20at%2009.04.27.jpeg)

## תיאור המאגר:
 בחרנו להשתמש במאגר מתוך ספריית datasets_tensorflow . 
 
 המאגר נקרא "rock_paper_scissors"ומכיל 2892 תמונות של ידיים המשחקות את המשחק "אבן נייר ומספריים" 

## מאפייני המאגר:
 למאגר שני מאפיינים – תמונה בגודל 300X300X3 , והתיוג שלה (אבן-1 ,נייר - 2 ,מספריים -3 )
 
 המאגר מחולק לtrain -המכיל 2520 תמונות, וtest -המכיל 372 תמונות.
 

## שאלת המאגר:
בהינתן תמונה חדשה המסמנת תנועת יד במשחק אבן נייר ומספרים – נרצה לדעת מה היד מסמנת.

## המודלים בהם השתמשנו:


#### -השתמשנו במודל אחד של למידת עמוקה:

א. CNN

#### -ובחמישה מודלים של למידת מכונה:

ב. Logistic Regression

ג.KNN

ד.Random Forest

ה. SVM

ו. Adaboost

## תהליך עיבוד התמונה:
 קיבלנו תמונה בגודל 300X300X3 (התמונה בגודל 300X300 פיקסלים ובפורמט RGB)

  ![](https://github.com/noahaim/Rock-paper-scissors/blob/8279b10dceb399d604562f477734a8ed48b150c0/WhatsApp%20Image%202022-02-11%20at%2009.09.59.jpeg)
  
1. שינינו את פורמט הRGB לפורמט One-Coloc-Channel כיוון שצבעי התמונה לא רלוונטים בשביל הקלסיפיקציה 
2. שינינו את גודל התמונה ל64X64 כדי לעזור למודל ללמוד יותר טוב את המידע ולא להעמיס עליו פרטים מיותרים שיצטרך ללמוד
3. נרמול הData לטווח 0-1 במקום 0-255 כדי להקל על המודל 

![](https://github.com/noahaim/Rock-paper-scissors/blob/d53d1ac76021ac7f53b69374b4db796c4b472002/image_after_proccecing.jpeg)

4.השארת גבולות האובייקט כמידע החיוני לקלסיפיקציה

![](https://github.com/noahaim/Rock-paper-scissors/blob/d53d1ac76021ac7f53b69374b4db796c4b472002/image_after_borders.jpeg)

## הקשיים שהיו לנו:
בתחילת האימון של המודלים שמו לב ששימוש בתמונות בגודלן המקורי לא מביא לנו תוצאות טובות אז החלטנו לשנות את גודל התמונות מ300X300 ל64X64.

זה שיפר לנו את התוצאות בצורה משמעותית מכיוון שהמודלים קיבלו כמות עצומה של מידע כאשר השתמשנו בתמונות בגודלן המקורי ולכן היה להם מאוד קשה להתאמן בלי לבצע over fitting

לאחר הקטנת כמות הפיקסלים שהמודל מקבל המודל יכול ללמוד את החשיבות של כל פיקסל בצורה משמעותית יותר כיוון שהפיקסל בעל משמעות רבה יותר .

הסיבה שהקטנת גודל הפקסלים לא פגעה בתוצאות של המודלים היא שבמאגר שלנו מספיק להסתכל על צורת היד באופן רחב יותר והפרטים הקטנים לא משנים לסיווג המחלקות.

קושי נוסף שהבחנו בו הוא שכאשר אנו רוצים לאמן מודלים של למידת מכונה (כמו Random Forest,KNN) כיוון שמודלים אלו לא מיועדים מלכתחילה לעיבוד תמונות נצטרך לשטח את המידע שהגיע בצורת פיקסלים(מטרציה דו מימדית) לוקטור אחד של ערכים.

פעולה זו גרמה לאיבוד קשרים משמעותיים בין פיקסלים והורידה בצורה ניכרת את ביצועי המודלים האלו.

לכן הוספנו מודל נוסף שמיועד לעיבוד תמונות - CNN שבנוי משכבות קונבולוציה המעבדות נוירונים.


## תוצאות המודלים ומסקנות:
לאחר צפייה בתוצאות המודלים החלטנו לנסות לשפר ולעבד יותר את הdata שקבלנו מהמאגר.
השתמשנו בפונקציה sobel מהספריה cv2 המיודעת לעיבוד תמונות.

מטרת הפונקציה היא להשאיר רק את הפקסלים של קצוות האובייקט(במקרה שלנו מסגרת כף היד) ובכך לאמן את הודל בצורה יותר טובה.

שמנו לב כי לא תמיד כלי זה עוזר לנו לשפר את התוצאות והחלטנו להריץ את המודלים פעם אחת רק לאחר ששיננו את גודל התמונה להיות 64X64X1 ופעם אחת גם לאחר שינוי הגודל והכלי הנוסף הזה.

התוצאות שקבלנו הראו שלא תמיד כלי זה באמת משפר את התוצאות ואנו חושבות שזה נובע מכך שלאחר השיטוח של המידע השארת גבולות האובייקט בלבד מקשות על המודלים מכייון שהקשרים בין פיקסלים קרובים לא נשמר כפי שציינו למעלה.

#### התוצאות לפניי שימוש בקצוות האובייקט:



![](https://github.com/noahaim/Rock-paper-scissors/blob/a2973aa04a67c7b012028284ccb1af2ea6612c0e/befor_border_results.jpeg)


#### התוצאות לאחר שימוש בגבולות האובייקט:



![](https://github.com/noahaim/Rock-paper-scissors/blob/a2973aa04a67c7b012028284ccb1af2ea6612c0e/after_borderd_results.jpeg)


## מסקנה סופית:
ניתן לראות על פי התוצאות שלא תמיד השארת גבולות התמונה כמידע העיקרי של האובייקט תעזור למודל ללמוד בצורה טובה יותר את המידע,

ניתן להבחין זאת במודלים של למידת מכונה, שלאחר השיטוח המודל מתקשה ללמוד את הגבולות של התמונות ולכן במודלים אלו התוצאות של אימון המודל על התמונות המלאות הצליח להשיג תוצאות טובות יותר.

לעומת זאת במודל למידה עמוקה לעיבוד התמונות שהוספנו ניתן לראות כי השארת גבולות האובייקט משפרת ומייעלת את למידת המודל וביצועיו.

בנוסף, נראה בבירור על פי הגרפים שתוצאות המודל CNN היו טובות יותר בצורה משמעותית לפי התחזית שלנו.
## תוצאות חדשות לאחר ההצגה:
הוספנו לאחר שיטוח התמונה את הטכניקה PCA שהיא טכניקה להפחתת מימד.

וכן ניתן לראות בתוצאות שאכן הצלחנו לשפר את התוצאות של המודלים של לימדת מכונה משמעותית מכיוון שהתמונות כבר לא רק עוברות לוקטור אחד  בשיטוח אלא נעזרות גם בPCA .

נסנו לשנות את הפונקציה בה השתמשנו למציאת השכנים הקרובים ולמצוא בעזרת פונקציה של מרחק מנהטן(סוכם את מספר הפיקסלים השונים בין התמונות) אך זה הוביל לתוצאות פחות טובות ולכן השארנו את הפונקציה שכבר היתה לנו.

הוספנו מודלים נוספים של למידת מכונה שהם-SVM ו Adaboost.
#### התוצאות לפניי שימוש בקצוות האובייקט:


![](https://github.com/noahaim/Rock-paper-scissors/blob/9cbb268940141bcf005c9256fae44707036ed9e6/new_results.JPG)

#### התוצאות לאחר שימוש בגבולות האובייקט:

![](https://github.com/noahaim/Rock-paper-scissors/blob/9cbb268940141bcf005c9256fae44707036ed9e6/new_results_B.JPG)
## מסקנות של התוצאות החדשות:
המודלים של למידת מכונה אכן השתפרו משמעותית כאשר השיטוח הוא יותר טוב ולא רק מעבר לוקטור אחד כי נאבדים פחות הקשרים בין הפסקלים.

בנוסף בתוצאות החדשות ניתן לראות שאכן השארת גבולות התמונה בלבד אכן משפרת את התוצאות במודל KNN לאחר שהוספנו את טכניקת PCA וגם בSVM התוצאות יותר טובות כאשר מתייחסים רק לגבולות התמונה מכיוון שיש פחות פרטים ולכן למודלים יותר קל לעבוד.

אך ניתן להבחין שגם לאחר ההוספות שעשינו עדיין נראה בבירור על פי הגרפים שתוצאות המודל CNN היו טובות יותר בצורה משמעותית.


