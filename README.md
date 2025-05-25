# kadai_Student.Management
課題で生徒の管理システム
package org.example;

//TIP コードを<b>実行</b>するには、<shortcut actionId="Run"/> を押すか
// ガターの <icon src="AllIcons.Actions.Execute"/> アイコンをクリックします。
import java.util.*;

public class Main {
    private static final Map<String, Integer> studentMap = new LinkedHashMap<>();
    private static final Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        boolean running = true;
        while (running) {
            printMenu();
            String choice = scanner.nextLine();

            switch (choice) {
                case "1" -> addStudent();
                case "2" -> removeStudent();
                case "3" -> updateScore();
                case "4" -> calculateAverage();
                case "5" -> displayAllStudents();
                case "6" -> {
                    System.out.println("プログラムを終了します");
                    running = false;
                }
                default -> System.out.println("無効な選択です。1〜6を入力してください。");
            }
        }
    }

    private static void printMenu() {
        System.out.println("\n1．学生を追加\n2．学生を削除\n3．点数を更新\n4．平均点を計算\n5．全学生の情報を表示\n6．終了");
        System.out.print("選択してください：");
    }

    private static void addStudent() {
        System.out.print("学生の名前を入力してください：");
        String name = scanner.nextLine();
        System.out.print(name + "の点数を入力してください：");
        try {
            int score = Integer.parseInt(scanner.nextLine());
            studentMap.put(name, score);
        } catch (NumberFormatException e) {
            System.out.println("点数は数値で入力してください。");
        }
    }

    private static void removeStudent() {
        System.out.print("学生の名前を入力してください：");
        String name = scanner.nextLine();
        if (studentMap.remove(name) != null) {
            System.out.println(name + "を削除しました");
        } else {
            System.out.println("学生が見つかりません。");
        }
    }

    private static void updateScore() {
        System.out.print("学生の名前を入力してください：");
        String name = scanner.nextLine();
        if (studentMap.containsKey(name)) {
            System.out.print(name + "の点数を入力してください：");
            try {
                int score = Integer.parseInt(scanner.nextLine());
                studentMap.put(name, score);
            } catch (NumberFormatException e) {
                System.out.println("点数は数値で入力してください。");
            }
        } else {
            System.out.println("学生が見つかりません。");
        }
    }

    private static void calculateAverage() {
        if (studentMap.isEmpty()) {
            System.out.println("学生が登録されていません。");
            return;
        }
        double average = studentMap.values().stream()
                .mapToInt(Integer::intValue)
                .average()
                .orElse(0);
        System.out.printf("平均点：%.1f点%n", average);
    }

    private static void displayAllStudents() {
        if (studentMap.isEmpty()) {
            System.out.println("学生が登録されていません。");
            return;
        }
        System.out.println("学生一覧：");
        studentMap.forEach((name, score) -> System.out.println(name + "：" + score + "点"));
    }//入力をGitHub上でReadmeを編集して上記プログラムを入力してみた。どうなるのかためします。
}