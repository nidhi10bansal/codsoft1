# 
#include <iostream> //create a to do list.
#include <vector>
#include <string>

using namespace std;
struct Task {
    string description;
    bool completed;

    Task(const string& desc) : description(desc), completed(false) {}
};
void addTask(vector<Task>& tasks, const string& description) {
    tasks.push_back(Task(description));
    cout << "Task added: " << description << endl;
}
void viewTasks(const vector<Task>& tasks) {
    if (tasks.empty()) {
        cout << "No tasks in the list." << endl;
        return;
    }

    for (size_t i = 0; i < tasks.size(); ++i) {
        cout << i + 1 << ". " << tasks[i].description
             << " [" << (tasks[i].completed ? "Completed" : "Pending") << "]" << endl;
    }
}
void markTaskCompleted(vector<Task>& tasks, size_t index) {
    if (index > 0 && index <= tasks.size()) {
        tasks[index - 1].completed = true;
        cout << "Task marked as completed: " << tasks[index - 1].description << endl;
    } else {
        cout << "Invalid task index." << endl;
    }
}
void removeTask(vector<Task>& tasks, size_t index) {
    if (index > 0 && index <= tasks.size()) {
        cout << "Task removed: " << tasks[index - 1].description << endl;
        tasks.erase(tasks.begin() + (index - 1));
    } else {
        cout << "Invalid task index." << endl;
    }
}

int main() {
    vector<Task> tasks;
    int choice;
    string description;
    size_t index;

    while (true) {
        cout << "\nTo-Do List Manager\n";
        cout << "1. Add Task\n";
        cout << "2. View Tasks\n";
        cout << "3. Mark Task as Completed\n";
        cout << "4. Remove Task\n";
        cout << "5. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Enter task description: ";
                cin.ignore();
                getline(cin, description);
                addTask(tasks, description);
                break;
            case 2:
                viewTasks(tasks);
                break;
            case 3:
                cout << "Enter task number to mark as completed: ";
                cin >> index;
                markTaskCompleted(tasks, index);
                break;
            case 4:
                cout << "Enter task number to remove: ";
                cin >> index;
                removeTask(tasks, index);
                break;
            case 5:
                cout << "Exiting!" << endl;
                return 0;
            default:
                cout << "Invalid. Please try again." << endl;
                break;
        }
    }

    return 0;
}
