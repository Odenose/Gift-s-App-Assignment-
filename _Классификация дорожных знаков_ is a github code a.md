#include <iostream>
#include <string>
#include <map>
#include <vector>

// Простейшая структура для "изображения" дорожного знака (заглушка)
struct TrafficSignImage {
std::string filePath; // путь к файлу изображения
int width;
int height;
// здесь могли бы быть пиксели, матрицы и т.д.
};

// Классы дорожных знаков
enum TrafficSignClass {
SPEED_LIMIT,
STOP_SIGN,
PEDESTRIAN_CROSSING,
TURN_RIGHT,
TURN_LEFT,
UNKNOWN_SIGN
};

// Словарь для вывода названия класса
std::map<TrafficSignClass, std::string> SIGN_NAMES = {
{SPEED_LIMIT, "Speed limit"},
{STOP_SIGN, "Stop"},
{PEDESTRIAN_CROSSING, "Pedestrian crossing"},
{TURN_RIGHT, "Turn right"},
{TURN_LEFT, "Turn left"},
{UNKNOWN_SIGN, "Unknown"}
};

// Простая "модель" классификатора дорожных знаков (заглушка)
class TrafficSignClassifier {
public:
TrafficSignClassifier() {
// Здесь могла бы быть загрузка обученной модели,
// чтение весов из файла и т.д.
}

    void initialize() {
        // Инициализация параметров модели, подготовка к классификации
        // Например, установка порогов, размер входного изображения и т.д.
        inputWidth = 32;
        inputHeight = 32;
        std::cout << "Traffic Sign Classifier initialized with input size "
                  << inputWidth << "x" << inputHeight << std::endl;
    }

    TrafficSignClass classify(const TrafficSignImage &img) {
        // Здесь обычно выполняется:
        // 1) Предобработка (resize, нормализация)
        // 2) Прогон через CNN / другую модель
        // 3) Выбор класса с максимальной вероятностью

        // Для учебного задания делаем простую заглушку по имени файла:
        if (img.filePath.find("speed") != std::string::npos) {
            return SPEED_LIMIT;
        } else if (img.filePath.find("stop") != std::string::npos) {
            return STOP_SIGN;
        } else if (img.filePath.find("pedestrian") != std::string::npos) {
            return PEDESTRIAN_CROSSING;
        } else if (img.filePath.find("right") != std::string::npos) {
            return TURN_RIGHT;
        } else if (img.filePath.find("left") != std::string::npos) {
            return TURN_LEFT;
        }
        return UNKNOWN_SIGN;
    }

private:
int inputWidth;
int inputHeight;
};

int main() {
// Инициализация "классификатора дорожных знаков"
TrafficSignClassifier classifier;
classifier.initialize();

    // Пример набора тестовых "изображений" дорожных знаков
    std::vector<TrafficSignImage> testImages = {
        {"images/speed_50.png", 64, 64},
        {"images/stop.png", 64, 64},
        {"images/pedestrian_crossing.jpg", 64, 64},
        {"images/turn_right.jpg", 64, 64},
        {"images/unknown_sign.bmp", 64, 64}
    };

    // "Классификация" дорожных знаков
    for (const auto &img : testImages) {
        TrafficSignClass cls = classifier.classify(img);
        std::cout << "File: " << img.filePath
                  << " -> class: " << SIGN_NAMES[cls] << std::endl;
    }

    return 0;

}
