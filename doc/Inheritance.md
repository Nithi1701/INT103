# Inheritance

> Inheritance คือการสืบทอดคุณสมบัติ จาก Model A ไปยัง Model อื่นๆได้ ซึ่งมันจะช่วยให้เราเพิ่มความสามารถใหม่ๆเข้าไปได้โดยที่ไม่ต้องไปยุ่งกับโค้ดเก่าที่เคยเขียนไว้
## ตัวอยย่าง

> สมมุติว่าเราต้องเขียน โปรแกรมบัญชีธนาคาร ซึ่งบัญชีออมทรัพย์สามารถเก็บข้อมูล เงินในบัญชี และ เจ้าของบัญชี ได้ และอย่าลืมนะว่าเราต้อง ฝากเงินเข้าบัญชี ได้ด้วย ดังนั้นเราก็น่าจะได้ Model ออกมาประมาณนี้

**Class SavingAccount**
```
public class SavingAccount {
    protected double balance;
    public double Balance;
    public String OwnerName;

    public SavingAccount(String OwnName){
        this.OwnerName = OwnName;
        this.balance = 0;
    }

    public void Deposit(double amount){
        if( amount > 0){
            balance += amount;
        }
    }

    public double getBalance() {
        return balance;
    }

    public String getOwnerName() {
        return OwnerName;
    }

    public void setOwnerName(String ownerName) {
        OwnerName = ownerName;
    }
}

```
**Class CurrentAccount**
```
public class CurrentAccount {
    protected double balance;
    public double Balance;
    public String OwnerName;

    public CurrentAccount(String OwnName){
        this.OwnerName = OwnName;
        this.balance = 0;
    }

    public void Deposit(double amount){
        if( amount > 0){
            balance += amount;
        }
    }

    public double getBalance() {
        return balance;
    }

    public String getOwnerName() {
        return OwnerName;
    }

    public void setOwnerName(String ownerName) {
        OwnerName = ownerName;
    }
}
```
> เราจะเห็นว่าโค้ด บัญชีออมทรัพย์ และ บัญชีกระแสรายวัน มันเหมือนกันเลย! ซึ่งถามว่าผิดไหม คำตอบคือไม่ผิดครับ แต่ถ้าเราปล่อยมันไว้แบบนี้เราจะมีปัญหาในอนาคต เช่น เรามาพบทีหลังว่าโค้ดมันเขียนผิดนะ แต่เราก็ copy ไปวางไว้ที่อื่นเรียบร้อยแล้ว
***

## การใช้ Inheritance แก้ปัญหา

>เราสามารถนำหลักการ Inheritance มาช่วยในเรื่องนี้ได้ โดยการสร้าง Model ต้นแบบ ขึ้นมา แล้วทำการย้ายของที่ซ้ำกันไปไว้ในตัวต้นแบบตัวนั้น ซึ่งในตัวอย่างของที่เรากำลังทำอยู่มันคือ บัญชีธนาคาร ดังนั้นเราเลยสร้างคลาส BankAccount ขึ้นมาใหม่

**Class BankAccount**
```
public class BankAccount {
    protected double balance;
    public double Balance;
    public String OwnerName;

    public BankAccount(String OwnName){
        this.OwnerName = OwnName;
        this.balance = 0;
    }

    public void Deposit(double amount){
        if( amount > 0){
            balance += amount;
        }
    }

    public double getBalance() { return balance; }

    public String getOwnerName() { return OwnerName; }

    public void setOwnerName(String ownerName) { OwnerName = ownerName; }
}

```
> แล้วทำการย้ายของที่มันซ้ำกันจาก บัญชีออมทรัพย์ กับ บัญชีกระแสรายวัน มาไว้ในตัว BankAccount แล้วนำเอาไป สืบทอด

**Class SavingAccount**
```
public class SavingAccount extends BankAccount {
    public SavingAccount(String OwnName){
        super(OwnName);
    }
}
```
**Class CurrentAccount**
```
public class CurrentAccount extends BankAccount {
    public CurrentAccount(String OwnName){
        super(OwnName);
    }
}
```
>เพียงเท่านี้ บัญชีออมทรัพย์ และ บัญชีกระแสรายวัน ก็จะมีความสามารถทุกอย่างที่ตัวต้นแบบมีนั่นเอง

# สรุป

> เราได้เห็นตัวอย่างโค้ดด้านบนไปแล้วว่า บัญชีออมทรัพย์ และ บัญชีกระแสรายวัน ได้ต่อยอดความสามารถจาก BankAccount มา เลยทำให้บัญชีทั้ง 2 ประเภทมี OwnerName, Balance และ Deposit() ทั้งๆที่ตัวมันเองไม่ได้มีโค้ดอะไรอยู่ด้านในเลย ซึ่งสิ่งนี้เราเรียกว่า การสืบทอด หรือ Inheritance นั่นเอง

### Base class (คลาสแม่)
> โดยคลาสที่เป็นต้นแบบเราเรียกมันว่า Base class (บางตำราจะเรียกว่า Super class, Parent class บลาๆ) ซึ่งในตัวอย่างนี้คลาส BankAccount เป็น base class ของ SavingAccount และ CurrentAccount นั่นเอง
### Sub class (คลาสลูก)
> ส่วนคลาสที่ไปสืบทอดความสามารถจากคนอื่นเราเรียกมันว่า Sub Class (บางตำราเรียกว่า Derived class, Child class บลาๆ) ซึ่งในตัวอย่างนี้คลาส SavingAccount และ CurrentAccount เป็น sub class ของ BankAccount นั่นเอง

### สิ่งที่ควรรู้
> ของที่อยู่ใน Base class จะถูกส่งลงมาให้ Sub class ส่วน sub class จะใช้มันได้หรือเปล่าขึ้นอยู่กับ accessibility ของ property พวกนั้น

### Override (การเปลี่ยนพฤติกรรม)
> อีกสิ่งหนึ่งที่เราได้จากการทำ Inheritance นั่นคือ เราสามารถทำให้การทำงานของ Sub class ทำงานแตกต่างกันกับ Base class ของมันได้ เช่น ตัวชัญชีนั้นจะต้องสามารถ ถอนเงิน ได้ ซึ่งจุดที่น่าสนใจของมันคือ

* **บัญชีออมทรัพย** - ถอนเงินได้สูงสุดไม่เกินเงินที่มีอยู่ในบัญชี
* **บัญชีกระแสรายวัน** - ถอนเงินได้เกินเงินที่มีอยู่ในบัญชี แต่ไม่เกินวงเงินที่ตั้งไว้

>ดังนั้นเราก็จะทำการเขียนโค้ดถอนเงินไว้ที่ตัว BankAccount ที่เป็น Base class ของมันก่อน ซึ่งได้ประมาณนี้

**Class BankAccount**
```
public class BankAccount {
    protected double balance;
    public double Balance;
    public String OwnerName;

    public BankAccount(String OwnName){
        this.OwnerName = OwnName;
        this.balance = 0;
    }

    public void Deposit(double amount){
        if( amount > 0){
            balance += amount;
        }
    }

    public void Withdraw(double amount)
    {
        if (amount <= balance)
        {
            balance -= amount;
        }
    }

    public double getBalance() { return balance; }

    public String getOwnerName() { return OwnerName; }

    public void setOwnerName(String ownerName) { OwnerName = ownerName; }
}
```
> เพียงเท่านี้เราก็จะสามารถถอนเงินได้ละ ส่วน บัญชีกระแสรายวัน เราก็ไปเขียนเพิ่มให้มันสามารถถอนเงินได้เกินเงินที่มี อยู่ในบัญชี ซึ่งสมมุติว่าวงเงินกู้ได้ไม่เกิน 1,000 ละกัน ดังนั้นเราก็จะได้โค้ดออกมาตามนี้

**Class SavingAccount**
```
public class SavingAccount extends BankAccount {

    private double credit = 1000;

    public SavingAccount(String OwnName){
        super(OwnName);
    }

    @Override
    public void Withdraw(double amount)
    {
        if (amount <= super.getBalance() + credit)
        {
            super.balance -= amount;
        }
    }
}

```

# ความสัมพันธ์แบบ Is a

เมื่อไหร่ก็ตามที่เราใช้ Inheritance ปุ๊ป เจ้าพวก Sub class ทั้งหลายจะมีความสัมพันธ์ที่เรียกว่า "Is a" ทันที หมายความว่า เราก็จะมองว่า บัญชีออมทรัพย์ และ บัญชีกระแสรายวัน มันเป็น บัญชีธนาคาร ประเภทหนึ่งทันที ซึ่งมันจะมีบทบาทที่สำคัญในเรื่องของการนำไปใช้กับ Polymorphism ในบทถัดไปอย่างมาก

> **ข้อควรระวัง** \
อย่าใช้ Inheritance เพราะเราขี้เกียจเขียนโค้ดซ้ำๆ เพราะมันจะได้ความสัมพันธ์แบบ Is A เข้าไปด้วย (เดี๋ยวไปดูความร้ายแรงของมันในบทของ Polymorphism เอาละกัน)

> **จงทำ Inheritance เมื่อ** \
Class พวกนั้นมันเป็นประเภทเดียวกันจริงๆ


# ลำดับชั้น
ในการทำ Inheritance มันจะมีลำดับชั้นความสัมพันธ์กันว่าใครเป็น คลาสแม่ คลาสลูก กันเสมอ ซึ่งจากโค้ดตัวอย่างด้านบนทั้งหมดก็สามารถเอามาเขียนเป็นแผนภาพ UML ง่ายๆได้ประมาณนี้

<p align="center">
  <img src="https://gblobscdn.gitbook.com/assets%2F-Lm0_idNbY6k1lwp6hm4%2F-M1lfqlFTvI3gmheTI_q%2F-M1lfv-2-JCTy1CgkFXy%2Fimage%20(952).png">
</p>

โดยเราจะเห็นว่า BankAccount เป็นคลาสแม่ ซึ่งมีลูก 2 ตัวคือ SavingAccount และ CurrentAccount

แต่มันยังไม่จบเพียงเท่านี้เพราะทุกคลาสจริงๆมันจะสืบสอดมาจากคลาสที่ชื่อว่า Object อีกที ดังนั้นแผนภาพที่แท้จริงคือ

<p align="center">
  <img src="https://gblobscdn.gitbook.com/assets%2F-Lm0_idNbY6k1lwp6hm4%2F-M1lfqlFTvI3gmheTI_q%2F-LnHTjrBaJiovB0IGWRf%2Fimage.png?alt=media">
</p>

ซึ่งจากรูปนี้คลาส BankAccount ก็เป็นคลาสลูกของคลาส Object อีกต่อหนึ่งนั่งเอง เลยทำให้มันมีความสามารถต่างๆของคลาสแม่ติดมาด้วยเสมอยังไงล่ะ

> **ที่มาข้อมูล:** 
 www.saladpuk.com