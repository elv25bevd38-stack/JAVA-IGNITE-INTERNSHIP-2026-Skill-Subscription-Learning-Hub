# DAY 1 — Backend Foundation

##  Goal
Understand Service Layer + CRUD operations

---

##  TASK 1: User Service

Implement in UserServiceImpl class:

### Methods:
- registerUser()
- login()

### Rules:
- Check duplicate email before register
- Validate password during login
- Return null if invalid
- import java.util.ArrayList;
import java.util.List;

public class UserServiceImpl implements UserService {

    private List<User> users = new ArrayList<>();

    @Override
    public boolean registerUser(User user) {

        // Check duplicate email
        for (User u : users) {
            if (u.getEmail().equalsIgnoreCase(user.getEmail())) {
                System.out.println("Email already exists!");
                return false;
            }
        }

        users.add(user);
        System.out.println("Registration Successful");
        return true;
    }

    @Override
    public User login(String email, String password) {

        // Validate email and password
        for (User u : users) {
            if (u.getEmail().equalsIgnoreCase(email)
                    && u.getPassword().equals(password)) {

                System.out.println("Login Successful");
                return u;
            }
        }

        System.out.println("Invalid Email or Password");
        return null;
    }
}

---

##  TASK 2: SkillPack Service

Implement in SkillPackServiceImpl:

### Methods:
- addSkillPack()
- getAllPacks()
- updateSkillPack()
- deleteSkillPack()

---

## Focus Areas

- Validation logic
- Repository usage
- Service layer thinking
- public interface SkillPackService {

    boolean addSkillPack(SkillPack pack);

    List<SkillPack> getAllPacks();

    boolean updateSkillPack(SkillPack pack);

    boolean deleteSkillPack(int id);

}
import java.util.List;

public class SkillPackServiceImpl implements SkillPackService {

    private SkillPackRepository repository;

    public SkillPackServiceImpl(SkillPackRepository repository) {
        this.repository = repository;
    }

    @Override
    public boolean addSkillPack(SkillPack pack) {

        // Validation
        if (pack == null) {
            return false;
        }

        if (pack.getName() == null || pack.getName().trim().isEmpty()) {
            System.out.println("Skill Pack Name cannot be empty");
            return false;
        }

        repository.save(pack);
        return true;
    }

    @Override
    public List<SkillPack> getAllPacks() {
        return repository.findAll();
    }

    @Override
    public boolean updateSkillPack(SkillPack pack) {

        // Validation
        if (pack == null) {
            return false;
        }

        SkillPack existingPack = repository.findById(pack.getId());

        if (existingPack == null) {
            System.out.println("Skill Pack not found");
            return false;
        }

        repository.update(pack);
        return true;
    }

    @Override
    public boolean deleteSkillPack(int id) {

        SkillPack existingPack = repository.findById(id);

        if (existingPack == null) {
            System.out.println("Skill Pack not found");
            return false;
        }

        repository.delete(id);
        return true;
    }
} 
import java.util.List;

public interface SkillPackRepository {

    void save(SkillPack pack);

    List<SkillPack> findAll();

    SkillPack findById(int id);

    void update(SkillPack pack);

    void delete(int id);
}
