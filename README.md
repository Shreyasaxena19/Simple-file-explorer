#include <stdio.h>
#include <dirent.h>
#include <unistd.h>  // For chdir function

void listFiles(const char *path) {
    struct dirent *de;
    DIR *dr = opendir(path);

    if (dr == NULL) {
        printf("Could not open directory %s\n", path);
        return;
    }

    printf("Contents of %s:\n", path);
    while ((de = readdir(dr)) != NULL)
        printf("%s\n", de->d_name);

    closedir(dr);
}

int main() {
    char path[100];
    printf("Enter the path to navigate: ");
    scanf("%s", path);

    fgets(path, sizeof(path), stdin);
    path[strcspn(path, "\n")] = 0; // Remove the newline character
    listFiles(path);

    return 0;
}
