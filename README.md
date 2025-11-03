#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <time.h>

struct URL {
    char original[100];
    char shortLink[10];
};

char randomChar() {
    char chars[] = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
    return chars[rand() % strlen(chars)];
}

void shorten(struct URL *url) {
    for (int i = 0; i < 6; i++)
        url->shortLink[i] = randomChar();
    url->shortLink[6] = '\0';
}

int main() {
    srand(time(0));
    struct URL urls[50];
    int count = 0, choice;

    while (1) {
        printf("\n1. Shorten URL\n2. View All\n3. Exit\nChoose: ");
        scanf("%d", &choice);

        if (choice == 1) {
            printf("Enter full URL: ");
            scanf("%s", urls[count].original);
            shorten(&urls[count]);
            printf("Short link: https://short.ly/%s\n", urls[count].shortLink);
            count++;
        } else if (choice == 2) {
            for (int i = 0; i < count; i++)
                printf("%s -> https://short.ly/%s\n", urls[i].original, urls[i].shortLink);
        } else if (choice == 3) break;
        else printf("Invalid.\n");
    }
    return 0;
}
