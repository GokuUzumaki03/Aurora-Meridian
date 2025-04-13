# Aurora-Meridian

Aurora Meridian Demo Code

import java.util.*;

public class MergedGame {

    // ---------------- Player Class ----------------
    static class Player {
        private Map<String, Integer> skills;
        private List<String> companions;

        public Player() {
            skills = new HashMap<>();
            companions = new ArrayList<>();

            // Example default skills
            skills.put("Stealth", 6);
            skills.put("Hacking", 4);
            skills.put("Firearms", 7);
            skills.put("Intimidation", 3);
            skills.put("Charisma", 5);
            skills.put("Intelligence", 6);
            skills.put("Strength", 5);
            skills.put("Unarmed", 7);
        }

        public int getSkill(String skill) {
            return skills.getOrDefault(skill, 0);
        }

        public void addCompanion(String name) {
            companions.add(name);
        }

        public List<String> getCompanions() {
            return companions;
        }
    }

    // ---------------- ScenarioManager Class ----------------
    static class ScenarioManager {
        private final Player player;

        public ScenarioManager(Player player) {
            this.player = player;
        }

        public void beginPrologue() {
            System.out.println("--- Prologue: The City of Aurora Meridian ---");
            System.out.println("You are Elias, a streetwise survivor in a decaying megacity...");
            System.out.println("Mysterious contacts whisper of a job that could change everything.");
            player.addCompanion("Benny");
            player.addCompanion("Miller");
            System.out.println("Benny and Miller have joined your crew.");
            presentHeistChoice();
        }

        private void presentHeistChoice() {
            Scanner scanner = new Scanner(System.in);
            System.out.println("Mission: Data Heist\nChoose your approach:");
            System.out.println("1. Stealth infiltration (requires Stealth or Hacking > 5)");
            System.out.println("2. Brute force entry (requires Firearms or Intimidation > 5)");
            int choice = scanner.nextInt();
            boolean success;
            switch (choice) {
                case 1:
                    success = (player.getSkill("Stealth") > 5 || player.getSkill("Hacking") > 5);
                    break;
                case 2:
                    success = (player.getSkill("Firearms") > 5 || player.getSkill("Intimidation") > 5);
                    break;
                default:
                    System.out.println("Invalid choice.");
                    return;
            }
            if (success) {
                System.out.println("Mission success: Data acquired. Rescue Mission unlocked.");
                rescueMission();
            } else {
                System.out.println("Mission failed: Security triggered. Convoy Ambush required.");
                convoyAmbush();
            }
        }

        private void rescueMission() {
            System.out.println("--- Mission: Rescue ---");
            System.out.println("A captured crew member must be extracted from a corporate outpost.");
            mission4();
        }

        private void convoyAmbush() {
            System.out.println("--- Mission: Convoy Ambush ---");
            System.out.println("You must raid a convoy or safehouse to recover from the failed heist.");
            mission4();
        }

        private void mission4() {
            System.out.println("--- Mission: Weapon Procurement Deal ---");
            System.out.println("You negotiate with black-market dealers Lawson and Ellison for firepower.");
            Scanner scanner = new Scanner(System.in);
            System.out.println("1. Inspect weapons (Firearms)");
            System.out.println("2. Haggle (Charisma)");
            System.out.println("3. Analyze risks (Intelligence)");
            int choice = scanner.nextInt();
            if (choice == 1 && player.getSkill("Firearms") > 5)
                System.out.println("You identify key weapons including a white phosphorus grenade.");
            if (choice == 2 && player.getSkill("Charisma") > 5)
                System.out.println("You negotiate a better deal.");
            if (choice == 3 && player.getSkill("Intelligence") > 5)
                System.out.println("You sense Ellison’s desperation and hidden motives.");
            mission5();
        }

        private void mission5() {
            System.out.println("--- Mission: Convoy Raid or Defensive Operation ---");
            System.out.println("Choose your next move:");
            System.out.println("1. Raid a convoy");
            System.out.println("2. Defend your safehouse");
            Scanner scanner = new Scanner(System.in);
            int choice = scanner.nextInt();
            if (choice == 1)
                System.out.println("You launch a high-stakes raid for augmentations and cyberware.");
            else
                System.out.println("You prepare defenses and repel a retaliatory strike.");
            mission6();
        }

        private void mission6() {
            System.out.println("--- Mission: Underground Arena or Blackmail Infiltration ---");
            System.out.println("You must now earn funds or leverage.");
            System.out.println("1. Fight in an underground arena (Strength/Unarmed)");
            System.out.println("2. Infiltrate an executive mansion (Stealth/Charisma)");
            Scanner scanner = new Scanner(System.in);
            int choice = scanner.nextInt();
            boolean success = false;

            if (choice == 1) {
                success = (player.getSkill("Strength") > 6 || player.getSkill("Unarmed") > 6);
                if (success)
                    System.out.println("Victory in the arena earns you cash and street cred.");
                else
                    System.out.println("You lose the fight and sustain injuries.");
            } else if (choice == 2) {
                success = (player.getSkill("Stealth") > 6 || player.getSkill("Charisma") > 6);
                if (success)
                    System.out.println("You extract valuable blackmail data from the mansion.");
                else
                    System.out.println("You're caught sneaking in and barely escape.");
            } else {
                System.out.println("Invalid choice.");
            }

            endPrologue();
        }

        private void endPrologue() {
            System.out.println("--- End of Prologue ---");
            System.out.println("Your journey through Aurora Meridian begins now.");
            System.out.println("Companions: " + String.join(", ", player.getCompanions()));
        }
    }

    // ---------------- Main Method ----------------
    public static void main(String[] args) {
        Player player = new Player();
        ScenarioManager scenarioManager = new ScenarioManager(player);
        scenarioManager.beginPrologue();
    }
}
