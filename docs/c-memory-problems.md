# Memory Problems 

## Filter  

Implement a program that applies filters to BMPs, per the below:  

```
$ ./filter -r image.bmp reflected.bmp
```

### **Background**  

Perhaps the simplest way to represent an image is with a grid of pixels (i.e., dots), each of which can be of a different color. For black-and-white images, we thus need 1 bit per pixel, as 0 could represent black and 1 could represent white, as in the below.

![bitmap](https://nicklyss.com/wp-content/uploads/2020/05/bitmap.png)  

In this sense, then, is an image just a bitmap (i.e., a map of bits). For more colorful images, you simply need more bits per pixel. A file format (like [BMP](https://en.wikipedia.org/wiki/BMP_file_format), [JPEG](https://en.wikipedia.org/wiki/JPEG), or [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics)) that supports “24-bit color” uses 24 bits per pixel. (BMP actually supports 1-, 4-, 8-, 16-, 24-, and 32-bit color.)

A 24-bit BMP uses 8 bits to signify the amount of red in a pixel’s color, 8 bits to signify the amount of green in a pixel’s color, and 8 bits to signify the amount of blue in a pixel’s color. If you’ve ever heard of RGB color, well, there you have it: red, green, blue.  

If the R, G, and B values of some pixel in a BMP are, say, `0xff`, `0x00`, and `0x00` in hexadecimal, that pixel is purely red, as `0xff` (otherwise known as `255` in decimal) implies “a lot of red,” while `0x00` and `0x00` imply “no green” and “no blue,” respectively.  


### **A Bit(map) More Technical**  

Recall that a file is just a sequence of bits, arranged in some fashion. A 24-bit BMP file, then, is essentially just a sequence of bits, (almost) every 24 of which happen to represent some pixel’s color. But a BMP file also contains some “metadata,” information like an image’s height and width. That metadata is stored at the beginning of the file in the form of two data structures generally referred to as “headers,” not to be confused with C’s header files. (Incidentally, these headers have evolved over time. This problem uses the latest version of Microsoft’s BMP format, 4.0, which debuted with Windows 95.)  

The first of these headers, called `BITMAPFILEHEADER`, is 14 bytes long. (Recall that 1 byte equals 8 bits.) The second of these headers, called `BITMAPINFOHEADER`, is 40 bytes long. Immediately following these headers is the actual bitmap: an array of bytes, triples of which represent a pixel’s color. However, BMP stores these triples backwards (i.e., as BGR), with 8 bits for blue, followed by 8 bits for green, followed by 8 bits for red. (Some BMPs also store the entire bitmap backwards, with an image’s top row at the end of the BMP file. But we’ve stored this problem set’s BMPs as described herein, with each bitmap’s top row first and bottom row last.) In other words, were we to convert the 1-bit smiley above to a 24-bit smiley, substituting red for black, a 24-bit BMP would store this bitmap as follows, where `0000ff` signifies red and `ffffff` signifies white; we’ve highlighted in red all instances of `0000ff`.  

![red-smile](https://nicklyss.com/wp-content/uploads/2020/05/red_smile.png)  

Because we’ve presented these bits from left to right, top to bottom, in 8 columns, you can actually see the red smiley if you take a step back.  

To be clear, recall that a hexadecimal digit represents 4 bits. Accordingly, ffffff in hexadecimal actually signifies 111111111111111111111111 in binary.  

Notice that you could represent a bitmap as a 2-dimensional array of pixels: where the image is an array of rows, each row is an array of pixels. Indeed, that’s how we’ve chosen to represent bitmap images in this problem.

### **Image Filtering**  

What does it even mean to filter an image? You can think of filtering an image as taking the pixels of some original image, and modifying each pixel in such a way that a particular effect is apparent in the resulting image.

**Grayscale**  

One common filter is the “grayscale” filter, where we take an image and want to convert it to black-and-white. How does that work?  

Recall that if the red, green, and blue values are all set to `0x00` (hexadecimal for `0`), then the pixel is black. And if all values are set to `0xff` (hexadecimal for `255`), then the pixel is white. So long as the red, green, and blue values are all equal, the result will be varying shades of gray along the black-white spectrum, with higher values meaning lighter shades (closer to white) and lower values meaning darker shades (closer to black).

So to convert a pixel to grayscale, we just need to make sure the red, green, and blue values are all the same value. But how do we know what value to make them? Well, it’s probably reasonable to expect that if the original red, green, and blue values were all pretty high, then the new value should also be pretty high. And if the original values were all low, then the new value should also be low.  

In fact, to ensure each pixel of the new image still has the same general brightness or darkness as the old image, we can take the average of the red, green, and blue values to determine what shade of grey to make the new pixel.  

If you apply that to each pixel in the image, the result will be an image converted to grayscale.

**Sepia**  

Most image editing programs support a “sepia” filter, which gives images an old-timey feel by making the whole image look a bit reddish-brown.  

An image can be converted to sepia by taking each pixel, and computing new red, green, and blue values based on the original values of the three.  

There are a number of algorithms for converting an image to sepia, but for this problem, we’ll ask you to use the following algorithm. For each pixel, the sepia color values should be calculated based on the original color values per the below.  

```
sepiaRed = .393 * originalRed + .769 * originalGreen + .189 * originalBlue
sepiaGreen = .349 * originalRed + .686 * originalGreen + .168 * originalBlue
sepiaBlue = .272 * originalRed + .534 * originalGreen + .131 * originalBlue
```  

Of course, the result of each of these formulas may not be an integer, but each value could be rounded to the nearest integer. It’s also possible that the result of the formula is a number greater than 255, the maximum value for an 8-bit color value. In that case, the red, green, and blue values should be capped at 255. As a result, we can guarantee that the resulting red, green, and blue values will be whole numbers between 0 and 255, inclusive.

**Reflection**

Some filters might also move pixels around. Reflecting an image, for example, is a filter where the resulting image is what you would get by placing the original image in front of a mirror. So any pixels on the left side of the image should end up on the right, and vice versa.  

Note that all of the original pixels of the original image will still be present in the reflected image, it’s just that those pixels may have rearranged to be in a different place in the image.  

**Blur**  

There are a number of ways to create the effect of blurring or softening an image. For this problem, we’ll use the “box blur,” which works by taking each pixel and, for each color value, giving it a new value by averaging the color values of neighboring pixels.  

Consider the following grid of pixels, where we’ve numbered each pixel.

![grid](https://nicklyss.com/wp-content/uploads/2020/05/grid.png)  

The new value of each pixel would be the average of the values of all of the pixels that are within 1 row and column of the original pixel (forming a 3x3 box). For example, each of the color values for pixel 6 would be obtained by averaging the original color values of pixels 1, 2, 3, 5, 6, 7, 9, 10, and 11 (note that pixel 6 itself is included in the average). Likewise, the color values for pixel 11 would be be obtained by averaging the color values of pixels 6, 7, 8, 10, 11, 12, 14, 15 and 16.  

For a pixel along the edge or corner, like pixel 15, we would still look for all pixels within 1 row and column: in this case, pixels 10, 11, 12, 14, 15, and 16.

### **Problem Solving**  

Get the files for the filter [HERE](https://cdn.cs50.net/2019/fall/psets/4/filter/less/filter.zip).  

Now let's look at the files provided to help break understand what is inside.  

**`bmp.h`**  
??? example "`bmp.h` code"
    ```c linenums="1"
    // BMP-related data types based on Microsoft's own

    #include <stdint.h>

    /**
     * Common Data Types
     *
     * The data types in this section are essentially aliases for C/C++
     * primitive data types.
     *
     * Adapted from http://msdn.microsoft.com/en-us/library/cc230309.aspx.
     * See http://en.wikipedia.org/wiki/Stdint.h for more on stdint.h.
     */
    typedef uint8_t  BYTE;
    typedef uint32_t DWORD;
    typedef int32_t  LONG;
    typedef uint16_t WORD;

    /**
     * BITMAPFILEHEADER
     *
     * The BITMAPFILEHEADER structure contains information about the type, size,
     * and layout of a file that contains a DIB [device-independent bitmap].
     *
     * Adapted from http://msdn.microsoft.com/en-us/library/dd183374(VS.85).aspx.
     */
    typedef struct
    {
        WORD   bfType;
        DWORD  bfSize;
        WORD   bfReserved1;
        WORD   bfReserved2;
        DWORD  bfOffBits;
    } __attribute__((__packed__))
    BITMAPFILEHEADER;

    /**
     * BITMAPINFOHEADER
     *
     * The BITMAPINFOHEADER structure contains information about the
     * dimensions and color format of a DIB [device-independent bitmap].
     *
     * Adapted from http://msdn.microsoft.com/en-us/library/dd183376(VS.85).aspx.
     */
    typedef struct
    {
        DWORD  biSize;
        LONG   biWidth;
        LONG   biHeight;
        WORD   biPlanes;
        WORD   biBitCount;
        DWORD  biCompression;
        DWORD  biSizeImage;
        LONG   biXPelsPerMeter;
        LONG   biYPelsPerMeter;
        DWORD  biClrUsed;
        DWORD  biClrImportant;
    } __attribute__((__packed__))
    BITMAPINFOHEADER;

    /**
     * RGBTRIPLE
     *
     * This structure describes a color consisting of relative intensities of
     * red, green, and blue.
     *
     * Adapted from http://msdn.microsoft.com/en-us/library/aa922590.aspx.
     */
    typedef struct
    {
        BYTE  rgbtBlue;
        BYTE  rgbtGreen;
        BYTE  rgbtRed;
    } __attribute__((__packed__))
    RGBTRIPLE;

    ```
You’ll see definitions of the headers we’ve mentioned (`BITMAPINFOHEADER` and `BITMAPFILEHEADER`). In addition, that file defines `BYTE`, `DWORD`, `LONG`, and `WORD`, data types normally found in the world of Windows programming. Notice how they’re just aliases for primitives with which you are (hopefully) already familiar. It appears that `BITMAPFILEHEADER` and `BITMAPINFOHEADER` make use of these types.  


Perhaps most importantly, this file also defines a `struct` called `RGBTRIPLE` that, quite simply, “encapsulates” three bytes: one blue, one green, and one red (the order, recall, in which we expect to find RGB triples actually on disk).

Why are these `struct`s useful? Well, recall that a file is just a sequence of bytes (or, ultimately, bits) on disk. But those bytes are generally ordered in such a way that the first few represent something, the next few represent something else, and so on. “File formats” exist because the world has standardized what bytes mean what. Now, we could just read a file from disk into RAM as one big array of bytes. And we could just remember that the byte at `array[i]` represents one thing, while the byte at `array[j]` represents another. But why not give some of those bytes names so that we can retrieve them from memory more easily? That’s precisely what the structs in `bmp.h` allow us to do. Rather than think of some file as one long sequence of bytes, we can instead think of it as a sequence of `struct`s.  

**`filter.c`**  

??? example "`filter.c` code"
    ```c linenums="1"
    #include <getopt.h>
    #include <stdio.h>
    #include <stdlib.h>

    #include "helpers.h"

    int main(int argc, char *argv[])
    {

        // Define allowable filters
        char *filters = "bgrs";

        // Get filter flag and check validity
        char filter = getopt(argc, argv, filters);
        if (filter == '?')
        {
            fprintf(stderr, "Invalid filter.\n");
            return 1;
        }

        // Ensure only one filter
        if (getopt(argc, argv, filters) != -1)
        {
            fprintf(stderr, "Only one filter allowed.\n");
            return 2;
        }

        // Ensure proper usage
        if (argc != optind + 2)
        {
            fprintf(stderr, "Usage: filter [flag] infile outfile\n");
            return 3;
        }

        // Remember filenames
        char *infile = argv[optind];
        char *outfile = argv[optind + 1];

        // Open input file
        FILE *inptr = fopen(infile, "r");
        if (inptr == NULL)
        {
            fprintf(stderr, "Could not open %s.\n", infile);
            return 4;
        }

        // Open output file
        FILE *outptr = fopen(outfile, "w");
        if (outptr == NULL)
        {
            fclose(inptr);
            fprintf(stderr, "Could not create %s.\n", outfile);
            return 5;
        }

        // Read infile's BITMAPFILEHEADER
        BITMAPFILEHEADER bf;
        fread(&bf, sizeof(BITMAPFILEHEADER), 1, inptr);

        // Read infile's BITMAPINFOHEADER
        BITMAPINFOHEADER bi;
        fread(&bi, sizeof(BITMAPINFOHEADER), 1, inptr);

        // Ensure infile is (likely) a 24-bit uncompressed BMP 4.0
        if (bf.bfType != 0x4d42 || bf.bfOffBits != 54 || bi.biSize != 40 ||
            bi.biBitCount != 24 || bi.biCompression != 0)
        {
            fclose(outptr);
            fclose(inptr);
            fprintf(stderr, "Unsupported file format.\n");
            return 6;
        }

        int height = abs(bi.biHeight);
        int width = bi.biWidth;

        // Allocate memory for image
        RGBTRIPLE(*image)[width] = calloc(height, width * sizeof(RGBTRIPLE));
        if (image == NULL)
        {
            fprintf(stderr, "Not enough memory to store image.\n");
            fclose(outptr);
            fclose(inptr);
            return 7;
        }

        // Determine padding for scanlines
        int padding = (4 - (width * sizeof(RGBTRIPLE)) % 4) % 4;

        // Iterate over infile's scanlines
        for (int i = 0; i < height; i++)
        {
            // Read row into pixel array
            fread(image[i], sizeof(RGBTRIPLE), width, inptr);

            // Skip over padding
            fseek(inptr, padding, SEEK_CUR);
        }

        // Filter image
        switch (filter)
        {
            // Blur
            case 'b':
                blur(height, width, image);
                break;

            // Grayscale
            case 'g':
                grayscale(height, width, image);
                break;

            // Reflection
            case 'r':
                reflect(height, width, image);
                break;

            // Sepia
            case 's':
                sepia(height, width, image);
                break;
        }

        // Write outfile's BITMAPFILEHEADER
        fwrite(&bf, sizeof(BITMAPFILEHEADER), 1, outptr);

        // Write outfile's BITMAPINFOHEADER
        fwrite(&bi, sizeof(BITMAPINFOHEADER), 1, outptr);

        // Write new pixels to outfile
        for (int i = 0; i < height; i++)
        {
            // Write row to outfile
            fwrite(image[i], sizeof(RGBTRIPLE), width, outptr);

            // Write padding at end of row
            for (int k = 0; k < padding; k++)
            {
                fputc(0x00, outptr);
            }
        }

        // Free memory for image
        free(image);

        // Close infile
        fclose(inptr);

        // Close outfile
        fclose(outptr);

        return 0;
    }

    ```  

First, notice the definition of `filters` on line 11. That string tells the program what the allowable command-line arguments to the program are: `b`, `g`, `r`, and `s`. Each of them specifies a different filter that we might apply to our images: blur, grayscale, reflection, and sepia.  

The next several lines open up an image file, make sure it’s indeed a BMP file, and read all of the pixel information into a 2D array called `image`.  

Scroll down to the `switch` statement that begins on line 102. Notice that, depending on what `filter` we’ve chosen, a different function is called: if the user chooses filter `b`, the program calls the `blur` function; if `g`, then `grayscale` is called; if `r`, then `reflect` is called; and if `s`, then `sepia` is called. Notice, too, that each of these functions take as arguments the height of the image, the width of the image, and the 2D array of pixels.

The remaining lines of the program take the resulting `image` and write them out to a new image file.

**`helpers.h`**  

??? example "`helpers.h` code"
    ```c linenums="1"
    #include "bmp.h"

    // Convert image to grayscale
    void grayscale(int height, int width, RGBTRIPLE image[height][width]);

    // Convert image to sepia
    void sepia(int height, int width, RGBTRIPLE image[height][width]);

    // Reflect image horizontally
    void reflect(int height, int width, RGBTRIPLE image[height][width]);

    // Blur image
    void blur(int height, int width, RGBTRIPLE image[height][width]);

    ```  
This file is quite short, and just provides the function prototypes for the functions you saw earlier.  

Here, take note of the fact that each function takes a 2D array called `image` as an argument, where `image` is an array of `height` many rows, and each row is itself another array of `width` many `GBTRIPLE`s. So if `image` represents the whole picture, then `image[0]` represents the first row, and `image[0][0]` represents the pixel in the upper-left corner of the image.  

**`helpers.c`**  

??? example "`helpers.c` code"
    ```c linenums="1"
    #include "helpers.h"

    // Convert image to grayscale
    void grayscale(int height, int width, RGBTRIPLE image[height][width])
    {
        return;
    }

    // Convert image to sepia
    void sepia(int height, int width, RGBTRIPLE image[height][width])
    {
        return;
    }

    // Reflect image horizontally
    void reflect(int height, int width, RGBTRIPLE image[height][width])
    {
        return;
    }

    // Blur image
    void blur(int height, int width, RGBTRIPLE image[height][width])
    {
        return;
    }

    ```  

Now, open up helpers.c. Here’s where the implementation of the functions declared in helpers.h belong. But note that, right now, the implementations are missing!  We will come back to this later.  

**`Makefile`**  

```
filter:
    clang -fsanitize=signed-integer-overflow -fsanitize=undefined -ggdb3 -O0 -Qunused-arguments -std=c11 -Wall -Werror -Wextra -Wno-sign-compare -Wno-unused-parameter -Wno-unused-variable -Wshadow -o filter filter.c helpers.c

```
Finally, let’s look at `Makefile`. This file specifies what should happen when we run a terminal command like `make filter`. Whereas programs you may have written before were confined to just one file, `filter` seems to use multiple files: `filter.c`, `bmp.h`, `helpers.h`, and `helpers.c`. So we’ll need to tell make how to compile this file.  

Try compiling `filter` for yourself by going to your terminal and running

```
$ make filter
```
Then, you can run the program by running:  

```
$ ./filter -g images/yard.bmp out.bmp
```  

which takes the image at `images/yard.bmp`, and generates a new image called `out.bmp` after running the pixels through the `grayscale` function. `grayscale` doesn’t do anything just yet, though, so the output image should look the same as the original yard.

### **Code and Solution**  

Here are our goals for the `filter` program:  

* The function `grayscale` should take an image and turn it into a black-and-white version of the same image.

* The function `sepia` should take an image and turn it into a sepia version of the same image.

* The `reflect` function should take an image and reflect it horizontally.

* Finally, the `blur` function should take an image and turn it into a box-blurred version of the same image.  

Let's look at `helpers.c` and add some code:  

??? example "`helpers.c` code"
    ```c linenums="1"
    #include "helpers.h"
    #include "math.h"
    #include "cs50.h"

    // Convert image to grayscale
    void grayscale(int height, int width, RGBTRIPLE image[height][width])
    {
        for (int i = 0; i < height; i++)
        {
            for (int j = 0; j < height; j++)
            {
                RGBTRIPLE pixel = image[i][j];
                int average = round((pixel.rgbtRed + pixel.rgbtBlue + pixel.rgbtGreen) / 3.0);
                image[i][j].rgbtRed = image[i][j].rgbtGreen = image[i][j].rgbtBlue = average;
            }
        }
    }

    // Convert image to sepia using formula given

    int capacity(int value)
    {
        return value > 255 ? 255 : value;
    }

    void sepia(int height, int width, RGBTRIPLE image[height][width])
    {
        for (int i = 0; i < height; i++)
        {
            for (int j = 0; j < height; j++)
            {
                RGBTRIPLE pixel = image[i][j];
                int originalRed = pixel.rgbtRed;
                int originalBlue = pixel.rgbtBlue;
                int originalGreen = pixel.rgbtGreen;
                image[i][j].rgbtRed = capacity(round(0.393 * originalRed + 0.769 * originalGreen + 0.189 * originalBlue));
                image[i][j].rgbtGreen = capacity(round(0.349 * originalRed + 0.686 * originalGreen + 0.168 * originalBlue));
                image[i][j].rgbtBlue = capacity(round(0.272 * originalRed + 0.534 * originalGreen + 0.131 * originalBlue));
            }
        }
    }
        // Reflect image horizontally
    void swap(RGBTRIPLE * pixel1, RGBTRIPLE * pixel2)
    {
        RGBTRIPLE temp = *pixel1;
        *pixel1 = *pixel2;
        *pixel2 = temp;
    }
        void reflect(int height, int width, RGBTRIPLE image[height][width])
    {
        for (int i = 0; i < height; i++)
        {
            for (int j = 0; j < width / 2; j++)
            {
                swap(&image[i][j], &image[i][width - 1 - i]);
            }
        }
    }
        // Blur image
    bool is_valid(int i, int j, int height, int width)
    {
        return i >= 0 && i < height && j >=0 && j < width;
    }

    RGBTRIPLE get_blur(int i, int j, int height, int width, RGBTRIPLE image[height][width])
    {
        int redValue, blueValue, greenValue; redValue = blueValue = greenValue = 0;
        int num_valid_pixels = 0;
        for (int di = -1; di <=1; di++) // di stand for change in i
        {
            for (int dj = -1; dj <=1; dj++)
            {
                int new_i = i + di;
                int new_j = j + dj;
                if (is_valid(new_i, new_j, height, width))
                {
                    num_valid_pixels++;
                    redValue += image[new_i][new_j].rgbtRed;
                    blueValue += image[new_i][new_j].rgbtBlue;
                    greenValue += image[new_i][new_j].rgbtGreen;
                }
            }
        }
        RGBTRIPLE blurred_pix;
        blurred_pix.rgbtRed = round((float)redValue / num_valid_pixels);
        blurred_pix.rgbtGreen = round((float)greenValue / num_valid_pixels);
        blurred_pix.rgbtBlue = round((float)blueValue / num_valid_pixels);
        return blurred_pix;
    }
        void blur(int height, int width, RGBTRIPLE image[height][width])
    {
        RGBTRIPLE blur_image[height][width];
        for (int i = 0; i < height; i++)
        {
            for (int j = 0; j < width; j++)
            {
                blur_image[i][j] = get_blur(i, j, height, width, image);
            }
        }
        for (int i = 0; i < height; i++)
            for (int j = 0; j < width; j++)
                image[i][j] = blur_image[i][j];
    }
    ```  

## Recover  

Implement a program that recovers JPEGs from a forensic image, per the below.  

```
$ ./recover card.raw
```  

### **Background**  

Sometimes, after taking an image, we may delete them by accident. Thankfully, in the computer world, “deleted” tends not to mean “deleted” so much as “forgotten.” Even though the camera insists that the card is now blank, we’re pretty sure that’s not quite true.  

Even though JPEGs are more complicated than BMPs, JPEGs have “signatures,” patterns of bytes that can distinguish them from other file formats. Specifically, the first three bytes of JPEGs are:  

```
0xff 0xd8 0xff
```  

from first byte to third byte, left to right. The fourth byte, meanwhile, is either `0xe0`, `0xe1`, `0xe2`, `0xe3`, `0xe4`, `0xe5`, `0xe6`, `0xe7`, `0xe8`, `0xe9`, `0xea`, `0xeb`, `0xec`, `0xed`, `0xee`, or `0xef`. Put another way, the fourth byte’s first four bits are `1110`.  

Odds are, if you find this pattern of four bytes on media known to store photos (e.g., my memory card), they demarcate the start of a JPEG. To be fair, you might encounter these patterns on some disk purely by chance, so data recovery isn’t an exact science.  

Fortunately, digital cameras tend to store photographs contiguously on memory cards, whereby each photo is stored immediately after the previously taken photo. Accordingly, the start of a JPEG usually demarks the end of another. However, digital cameras often initialize cards with a FAT file system whose “block size” is 512 bytes (B). The implication is that these cameras only write to those cards in units of 512 B. A photo that’s 1 MB (i.e., 1,048,576 B) thus takes up 1048576 ÷ 512 = 2048 “blocks” on a memory card. But so does a photo that’s, say, one byte smaller (i.e., 1,048,575 B)! The wasted space on disk is called “slack space.” Forensic investigators often look at slack space for remnants of suspicious data.  

The implication of all these details is that you, the investigator, can probably write a program that iterates over a copy of my memory card, looking for JPEGs’ signatures. Each time you find a signature, you can open a new file for writing and start filling that file with bytes from my memory card, closing that file only once you encounter another signature. Moreover, rather than read my memory card’s bytes one at a time, you can read 512 of them at a time into a buffer for efficiency’s sake. Thanks to FAT, you can trust that JPEGs’ signatures will be “block-aligned.” That is, you need only look for those signatures in a block’s first four bytes.  

Realize, of course, that JPEGs can span contiguous blocks. Otherwise, no JPEG could be larger than 512 B. But the last byte of a JPEG might not fall at the very end of a block. Recall the possibility of slack space. But not to worry. Because this memory card was brand-new when I started snapping photos, odds are it’d been “zeroed” (i.e., filled with 0s) by the manufacturer, in which case any slack space will be filled with 0s. It’s okay if those trailing 0s end up in the JPEGs you recover; they should still be viewable.  
Now, I only have one memory card, but there are a lot of you! And so I’ve gone ahead and created a “forensic image” of the card, storing its contents, byte after byte, in a file called `card.raw`. So that you don’t waste time iterating over millions of 0s unnecessarily, I’ve only imaged the first few megabytes of the memory card. But you should ultimately find that the image contains 50 JPEGs.  

### **Problem Solving**

Get the files for the recovery problem [HERE](https://cdn.cs50.net/2019/fall/psets/4/recover/recover.zip).  

Let's take a look at the code provided in the .zip:  

??? example "`recover.c` code"
    ```c linenums="1"
    #include <stdio.h>
    #include <stdlib.h>

    int main(int argc, char *argv[])
    {

    }
    ```
The above code is basically bare of anything, which means we should break down what we need to do:  

**Tasks**  

* Open memory card  

* Look for beginning of a JPEG  

* Open a new JPEG file  

* Write 512 bytes until a new JPEG is found  

* Stop at the end of the file  

Let's look at some things we can do for each step:  

**Open memory card**

We can take advantage of the `fopen()` function to open the memory card:  

```c
FILE *f = fopen(filename, "r");
```
Here inside the `fopen();` the filename is the name of the file you are trying to open and the `"r"` means you want to read the files.  

**Look for beginning of a JPEG**  

As mentioned previously, each JPEG file starts with a distinct header, meaning that first byte is always `0xff`, the second byte is always `0xd8`, the third byte is always `0xff`, and the fourth byte can vary a little bit, but always start with `0xe`.  

Luckily for us, each JPEG is stored back-to-back in this problem file.  

We can utilize the `fread()` function to look for JPEGs.  

```c
fread(data, size, number, inptr);
```
The above code can be broken down as:  

* `data`: pointer to where to store data you're reading.

* `size`: size of each element to read.

* `number`: number of elements to read.

* `inptr`: `FILE *` to read from.  

For example, we can check to see if the first byte of an array, for example called `buffer`, contains `0xff`:  

```c
buffer[0] == 0xff
buffer[1] == 0xd8
buffer[2] == 0xff
```
`buffer[3]` is a little bit more confusing because it can vary.  We could use a boolean expression here to check all the different variations to start:  

```c
buffer[3] == 0xe0 || buffer[3] == 0xe1 || buffer[3] == 0xe2
...
```
But having to write out all 16 variations could become tedious.  For a shortcut, we could use bitwise arithmatic:  

```c
(buffer[3] & 0xf0) == 0xe0
```
This is going to say to look at the first 4 bits of this 8 bit byte, and set the remaining 4 bytes to zero.  This clears out the last 4 bits and compares the results.  

**Open a new JPEG file**  

After we find a JPEG, we need to make a new JPEG file.  To begin we need to have filenames set as `###.jpg`, starting at `000.jpg`.  This will help us keep track of the number of JPEGs found.  

We can utilize the `sprintf()` function here, where instead of printing to the terminal, it prints to a `string`.  

For example, we could use the following code:  

```c
sprintf(filename, "%03i.jpg", 2);
```  
`%03i.jpg` simply means to print an integer with 3 digits.  

Next, to create the new file, we can use the `fopen()` function again:  

```c
FILE *img = fopen(filename, "w");
```
Notice the `"w"`, which stands for write.  

To begin writing the new file, we can use the `fwrite` function:  

```c
fwrite(data, size, number, outptr);
```
The above code can be broken down as:  

* `data`: pointer to bytes that will be written to file.

* `size`: size of each element to write.

* `number`: number of elements to write.

* `outptr`: `FILE *` to write to.  

* Returns number of items of size `size` were read.  

**Pseudocode**  
```
Open memory card
Repeat until end of card: 
    Read 512 bytes into a buffer
    If start of new JPEG
        If first JPEG
            ...
        Else
            ...
    Else
        If already found JPEG
```
### Solution  

??? example "`recover.c` code"
    ```c linenums="1"
    #include <stdio.h>
    #include <stdlib.h>
    #include <cs50.h>
    #include <stdint.h>
    typedef uint8_t BYTE; //defining BYTE as a byte (unsigned integer of length = 8 bits)
    #define BLOCK_SIZE 512 // setting BLOCK_SIZE to 512 bytes
    #define FILE_NAME_SIZE 8
    bool start_jpeg(BYTE buffer[]);

    int main(int argc, char *argv[])
    {
        if (argc !=2)
        {
            printf("Usage: ./recover image\n");
            return 1;
        }
        FILE* infile = fopen(argv[1], "r")
        if (infile == NULL)
        {
            printf("File not found\n");
            return 1;
        }

        BYTE buffer[BLOCK_SIZE];
        int file_index = 0;
        bool first_jpeg = false;
        FILE* outfile;
        while (fread(buffer, BLOCK_SIZE, 1, infile))
        {
            if (start_jpeg(buffer))
            {
                if (!first_jpeg)
                    first_jpeg = true;
                else
                    fclose(outfile);

                char filename(FILE_NAME_SIZE);
                sprintf(filename, "%03i.jpg", file_index++);
                outfile = fopen(filename, "w");
                if (outfile == NULL)
                    return 1;
                fwrite(buffer, BLOCK_SIZE, 1, outfile);
            }

            else if (first_jpeg)
            {
                fwrite(buffer, BLOCK_SIZE, 1, outfile)
            }
        }
        fclose(outfile);
        fclose(infile);

    }

    bool start_jpeg(BYTE buffer[])
    {
        return buffer[0] == 0xff && buffer[1] == 0xd8 && buffer[2] == 0xff && (buffer[3] & 0xf0) == 0xe0;

    }
    ```