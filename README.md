class DecisionTree:
    def __init__(self, knowledge_base):
        self.knowledge_base = knowledge_base

    def ask_question(self, current_node):
        if isinstance(current_node, dict):
            for question, answers in current_node.items():
                print(question)
                answer = input("Enter Yes or No: ").capitalize()

                if answer in answers:
                    return self.ask_question(answers[answer])
                else:
                    print("Invalid input! Please enter Yes or No.")
                    return self.ask_question(current_node)
        else:
            print(f"Diagnosis: {current_node}")
            return current_node


if __name__ == "__main__":
    K_Base = {
        "Is the computer powering on?": {
            "Yes": {
                "Is there a beeping sound?": {
                    "Yes": "Check the RAM and CPU",
                    "No": {
                        "Is the display showing any output?": {
                            "Yes": "Check the display connections and settings",
                            "No": "Check the power supply and motherboard"
                        }
                    }
                }
            },
            "No": "Check the power supply and cables"
        }
    }

    decision_tree = DecisionTree(K_Base)
    decision_tree.ask_question(K_Base)

