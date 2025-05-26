## 📦 倉庫物品追跡プログラム（チーム「チドン」）

### 📝 プロジェクト概要

このプロジェクトは、物流業務における倉庫管理システムを学び、Javaを使用して入出庫が可能な在庫管理プログラムをチームで構築することを目的とした協働学習です。

---

### 👥 チーム構成

| 名前     | 学科            | 学年 |
|----------|-----------------|------|
| 이미림   | ソフトウェア学科 | 4年  |
| 최자연   | ソフトウェア学科 | 4年  |
| 김경진   | ソフトウェア学科 | 1年  |
| 선병길   | 国際物流学科     | 4年  |
| 신지수   | 国際物流学科     | 1年  |

---

### 🎯 活動目標

- 倉庫管理の流れと仕組みを理解する  
- プログラミングを用いたシステム構築スキルを習得する  
- 他学科の学生と協力して課題を解決する力を養う

---

### 🛠 使用技術

- プログラミング言語：**Java**  
- 構成要素：クラス、メンバ変数、メソッド、入出力処理

---

### 🗓 週別活動内容
-第1週：チーム紹介、役割分担、テーマ決定

-第2週：倉庫管理の基本プロセスと物流用語の学習

-第3週：先進事例の調査と応用可能性の検討

-第4週：実装計画の策定とクラス設計

-第5週：Javaによるコーディングとデバッグ、テスト


---
✨ 学びと成長
- 本プロジェクトでは、異なる専攻の学生と協力し、物流とITを融合した学習を行うことができました。
- Javaのオブジェクト指向設計を取り入れ、効率的なクラス設計と役割分担を通して、協働の大切さを実感しました。

---
🏁 成果物まとめ
- 完成物：Javaによる簡易在庫管理システム

- 主な機能：入庫、出庫、残高確認

- 形式：GUIなし（コンソールベース）

---

### 📄 実装コード（抜粋）
<details> <summary><b>📦 コード全文を見る</b></summary> <div markdown="1">

```java
// Goods.java
public class Goods {
    public String GoodsNo; // 商品番号
    public String name;    // 商品名
    public int age;        // 保管年数
    public String phoneNo; // 位置番号
}
  ``` 
```java
// Utility.java
import java.util.Scanner;

public class Utility {
    static Scanner sc = new Scanner(System.in);

    public static int inputNumber() {
        return Integer.parseInt(sc.nextLine());
    }

    public static String inputString() {
        return sc.nextLine();
    }
}

  ```
```java
// GoodsSort.java
public class GoodsSort {
    private static Goods[] GoodsArr;

    public static void main(String[] args) {
        createGoodsInfoFromInput();
        printGoodsInfo("[入力された商品情報]");
        SortGoodsInfoByAgeDesc();
        printGoodsInfo("[年齢降順ソート結果]");
        SortGoodsInfoByName();
        printGoodsInfo("[商品名昇順ソート結果]");
        while(SearchGoodsByName());
        System.out.println("\n#プログラムを終了します。");
    }

    private static void createGoodsInfoFromInput() {
        System.out.print(">> 登録する商品の数を入力してください: ");
        int numOfGoods = Utility.inputNumber();
        GoodsArr = new Goods[numOfGoods];

        for (int i = 0; i < GoodsArr.length; i++) {
            GoodsArr[i] = new Goods();
            System.out.println("[" + (i + 1) + "番目の商品情報入力]");
            System.out.print("商品番号: ");
            GoodsArr[i].GoodsNo = Utility.inputString();
            System.out.print("商品名: ");
            GoodsArr[i].name = Utility.inputString();
            System.out.print("年齢: ");
            GoodsArr[i].age = Utility.inputNumber();
            System.out.print("商品位置番号: ");
            GoodsArr[i].phoneNo = Utility.inputString();
            System.out.println();
        }
        System.out.println();
    }

    private static void printGoodsInfo(String title) {
        System.out.println(title);
        System.out.println("--------------------------------------------");
        System.out.println("商品番号\t商品名\t年齢\t商品位置番号");
        System.out.println("--------------------------------------------");
        for(Goods Goods : GoodsArr) {
            System.out.print(Goods.GoodsNo + "\t");
            System.out.print(Goods.name + "\t");
            System.out.print(Goods.age + "\t");
            System.out.println(Goods.phoneNo);
        }
        System.out.println("--------------------------------------------\n");
    }

    private static void SortGoodsInfoByName() {
        for (int i = 0 ; i < GoodsArr.length-1 ; i++) {
            for (int j = i+1 ; j < GoodsArr.length ; j++) {
                if(GoodsArr[i].name.compareTo(GoodsArr[j].name) > 0) {
                    Goods temp = GoodsArr[j];
                    GoodsArr[j] = GoodsArr[i];
                    GoodsArr[i] = temp;
                }
            }
        }
    }

    private static void SortGoodsInfoByAgeDesc() {
        for (int i = 0 ; i < GoodsArr.length-1 ; i++) {
            for (int j = i+1 ; j < GoodsArr.length ; j++) {
                if (GoodsArr[i].age < GoodsArr[j].age) {
                    Goods temp = GoodsArr[j];
                    GoodsArr[j] = GoodsArr[i];
                    GoodsArr[i] = temp;
                }
            }
        }
    }

    private static boolean SearchGoodsByName() {
        System.out.print(">> 検索する商品の商品番号を入力してください（終了：q）: ");
        String GoodsNo = Utility.inputString();

        if (GoodsNo.equals("q")) {
            return false;
        }

        boolean found = false;
        for (Goods g : GoodsArr) {
            if(GoodsNo.equals(g.GoodsNo)) {
                System.out.println("--------------------------------------------");
                System.out.println("商品名         : " + g.name);
                System.out.println("年 齢          : " + g.age);
                System.out.println("商品位置番号  : " + g.phoneNo);
                System.out.println("--------------------------------------------");
                found = true;
                break;
            }
        }

        if (!found) {
            System.out.println("商品番号 " + GoodsNo + " に一致する商品は存在しません！");
        }

        return true;
    }
}
 ```
</div> </details>
