#include <iostream>
#include <vector>

template <typename T>
struct Node {
	T data;
	Node* right;
	Node* left;
};

template <typename T>
class BST {
private:
	std::vector<T> result;
	
	Node<T>* makeNewNode(T data) {
		Node<T>* new_node = new Node<T>();
		new_node->data = data;
		new_node->left = nullptr;
		new_node->right = nullptr;

		return new_node;
	}

public:
	Node<T>* insert(Node<T>* root, T input_number) {
		if (root == nullptr) {
			root = makeNewNode(input_number);
		}
		else if (root->data >= input_number) {
			root->left = insert(root->left, input_number);
		}
		else {
			root->right = insert(root->right, input_number);
		}
		return root;
	}

	void sort(Node<T>* root) {
		if (root != nullptr) {
			sort(root->left);
			result.push_back(root->data);
			sort(root->right);
		}	
	}

	const void printRes() const {
		for (T var : result) {
			std::cout << var << ",  ";
		}
	}
};


int main(int argc, char* argv[]) {
	BST<float>* tree = new BST<float>;
	Node<float>* root = nullptr;	

	float input_list[] = { 2, 0, 1.12, 33.78, 454.11, 122.02, 3.78, 1.01, 989.7, 1000.009, 1.02, 1, 1.03, 342, 200, 45, 23, 15, 14.99, 999 };

	for (size_t i = 0; i < (sizeof(input_list) / sizeof(int)); i++){
		root = tree->insert(root, input_list[i]);
	}

	tree->sort(root);
	tree->printRes();
	
	char pause;
	std::cin >> pause;
	return 0;
}