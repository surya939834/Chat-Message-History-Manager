#include <iostream>
#include <stack>
#include <queue>
#include <string>
#include <chrono>
#include <ctime>
#include <iomanip>

using namespace std;


struct ChatMessage {
    string content;
    time_t timestamp;

    ChatMessage(string msg) {
        content = msg;
        timestamp = time(nullptr); // current time
    }

    void display() const {
        cout << "[" << put_time(localtime(&timestamp), "%Y-%m-%d %H:%M:%S") << "] " << content << endl;
    }
};

class ChatManager {
private:
    queue<ChatMessage> incomingMessages;
    stack<ChatMessage> undoStack;
    stack<ChatMessage> redoStack;

public:
    
    void sendMessage(const string& msg) {
        ChatMessage message(msg);
        incomingMessages.push(message);
        undoStack.push(message);
        
        while (!redoStack.empty()) redoStack.pop();
        cout << "Sent: ";
        message.display();
    }

   
    void undo() {
        if (undoStack.empty()) {
            cout << "Nothing to undo.\n";
            return;
        }
        ChatMessage message = undoStack.top();
        undoStack.pop();
        redoStack.push(message);
        cout << "Undo: ";
        message.display();
    }


    void redo() {
        if (redoStack.empty()) {
            cout << "Nothing to redo.\n";
            return;
        }
        ChatMessage message = redoStack.top();
        redoStack.pop();
        undoStack.push(message);
        cout << "Redo: ";
        message.display();
    }

    void displayAllMessages() {
        cout << "\n--- Message History ---\n";
        queue<ChatMessage> temp = incomingMessages;
        while (!temp.empty()) {
            temp.front().display();
            temp.pop();
        }
    }
};

int main() {
    ChatManager chat;

    chat.sendMessage("Hello, world!");
    chat.sendMessage("How are you?");
    chat.undo();
    chat.redo();
    chat.displayAllMessages();

    return 0;
}
