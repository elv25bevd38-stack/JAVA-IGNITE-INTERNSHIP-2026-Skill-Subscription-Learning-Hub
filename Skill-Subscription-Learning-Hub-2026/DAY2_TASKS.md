# DAY 2 — Subscription System (CORE LOGIC DAY)

##  Goal
Build real-world subscription flow

---

##  TASK 1: Subscribe User

Implement:

- subscribe(userId, packId)

### Steps:
- Fetch user from DB
- Fetch skill pack
- Validate both exist
- Create Subscription object
- Set:
  - startDate = today
  - endDate = today + 30 days
  - status = "ACTIVE"
- Save subscription

import java.time.LocalDate;

public boolean subscribe(int userId, int packId) {

    // Fetch user
    User user = userRepository.findById(userId);

    if (user == null) {
        System.out.println("User not found");
        return false;
    }

    // Fetch skill pack
    SkillPack pack = skillPackRepository.findById(packId);

    if (pack == null) {
        System.out.println("Skill Pack not found");
        return false;
    }

    // Create subscription
    Subscription subscription = new Subscription();

    subscription.setUser(user);
    subscription.setSkillPack(pack);

    // Set dates
    LocalDate today = LocalDate.now();

    subscription.setStartDate(today);
    subscription.setEndDate(today.plusDays(30));

    // Set status
    subscription.setStatus("ACTIVE");

    // Save subscription
    subscriptionRepository.save(subscription);

    System.out.println("Subscription created successfully");

    return true;
} 

User findById(int userId);

SkillPack findById(int packId);

void save(Subscription subscription);---

##  TASK 2: Get User Subscriptions

Implement:

- getUserSubscriptions(userId)

---

##  Focus Areas

- Entity relationships
- Business logic design
- Date handling
- import java.time.LocalDate;
import java.util.List;

@Override
public List<Subscription> getUserSubscriptions(int userId) {

    // Check if user exists
    User user = userRepository.findById(userId);

    if (user == null) {
        System.out.println("User not found");
        return null;
    }

    // Get all subscriptions of the user
    List<Subscription> subscriptions =
            subscriptionRepository.findByUserId(userId);

    // Update status based on expiry date
    LocalDate today = LocalDate.now();

    for (Subscription sub : subscriptions) {

        if (sub.getEndDate().isBefore(today)) {
            sub.setStatus("EXPIRED");
        }
    }

    return subscriptions;
} 
List<Subscription> findByUserId(int userId);
import java.time.LocalDate;

public class Subscription {

    private int id;
    private User user;
    private SkillPack skillPack;
    private LocalDate startDate;
    private LocalDate endDate;
    private String status;

    // getters and setters
}
