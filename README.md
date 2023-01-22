0x11. C - printf team project

Group Project:                                                                      
                                                                                    
0. I'm not going anywhere. You can print that wherever you want to. I'm here and I'm
 a Spur for life                                                                    
Write a function that produces output according to a format.                        
                                                                                    
                                                                                    
1. Education is when you read the fine print. Experience is what you get if you don'
t                                                                                   
Handle the following conversion specifiers:

2. With a face like mine, I do better in print                                      
Handle the following custom conversion specifiers:                                  
                                                                                    
3. What one has not experienced, one will never understand in print                 
Handle the following conversion specifiers:                                         
                                                                                    
4. Nothing in fine print is ever good news                                          
Use a local buffer of 1024 chars in order to call write as little as possible.      
                                                                                    
5. My weakness is wearing too much leopard print                                    
Handle the following custom conversion specifier:                                   
                                                                                    
6. How is the world ruled and led to war? Diplomats lie to journalists and believe t
hese lies when they see them in print                                               
Handle the following conversion specifier: p.                                       
                                                                                    
7. The big print gives and the small print takes away                               
Handle the following flag characters for non-custom conversion specifiers:          
                                                                                    
8. Sarcasm is lost in print                                                         
Handle the following length modifiers for non-custom conversion specifiers:         
                                                                                    
l                                                                                   
h                                                                                   
Conversion specifiers to handle: d, i, u, o, x, X                                   
                                                                                    
9. Print some money and give it to us for the rain forests                          
Handle the field width for non-custom conversion specifiers.                        
                                                                                    
10. The negative is the equivalent of the composer's score, and the print the perfor
mance                                                                               
Handle the precision for non-custom conversion specifiers.                          
                                                                                    
11. It's depressing when you're still around and your albums are out of print       
Handle the 0 flag character for non-custom conversion specifiers.                   
                                                                                    
12. Every time that I wanted to give up, if I saw an interesting textile, print what
 ever, suddenly I would see a collection                                            
Handle the - flag character for non-custom conversion specifiers.                   
                                                                                    
13. Print is the sharpest and the strongest weapon of our party                     
Handle the following custom conversion specifier:                                   
                                                                                    
14. The flood of print has turned reading into a process of gulping rather than savo
ring                                                                                
Handle the following custom conversion specifier:                                   
                                                                                    
15. *                                                                               
All the above options work well together. 


========================================

_printf.c CODE


#include "main.h"

void print_buffer(char buffer[], int *buff_ind);

/**
 * _printf - Printf function
 * @format: format.
 * Return: Printed chars.
 */
int _printf(const char *format, ...)
{
	int i, printed = 0, printed_chars = 0;
	int flags, width, precision, size, buff_ind = 0;
	va_list list;
	char buffer[BUFF_SIZE];

	if (format == NULL)
	   return (-1);

	   va_start(list, format);

	   for (i = 0; format && format[i] != '\0'; i++)
	   {
		if (format[i] != '%')
		   {
				buffer[buff_ind++] = format[i];
						     if (buff_ind == BUFF_SIZE)
						     		     print_buffer(buffer, &buff_ind);
												/* write(1, &format[i], 1);*/
												   	    printed_chars++;
														}
															else
																{
																		print_buffer(buffer, &buff_ind);
																					flags = get_flags(format, &i);
																					      	width = get_width(format, &i, list);
																						      	precision = get_precision(format, &i, list);
																								    size = get_size(format, &i);
																								    	   ++i;
																											printed = handle_print(format, &i, list, buffer,
																												  		       flags, width, precision, size);
																														       	      	     if (printed == -1)
																																     		    return (-1);
																																				printed_chars += printed;
																																					      }
																																					      }

																																					      print_buffer(buffer, &buff_ind);

																																					      va_end(list);

																																					      return (printed_chars);
}

/**
 * print_buffer - Prints the contents of the buffer if it exist
 * @buffer: Array of chars
 * @buff_ind: Index at which to add next char, represents the length.
 */
void print_buffer(char buffer[], int *buff_ind)
{
	if (*buff_ind > 0)
	   write(1, &buffer[0], *buff_ind);

	   *buff_ind = 0;
}

