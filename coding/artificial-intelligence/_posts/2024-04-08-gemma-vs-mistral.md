#  Playing with open source LLM : Gemma vs Mistral
 
 In this article, I will compare the responses Mistral and Gemma provided to the same questions I asked them.
 I have run those two models separately on my personal computer which is a DELL G15 with an NVIDIA GeForce RTX 3060 with CUDA version 12.2.
 In another article, I compared the same two models on my Macbook Pro M3 PRO.
 
 To run those two models I used Ollama which is an open-source tool created to make LLMs ease of access to any user in the world. In another arcticle, I explained how to download Ollama and use it to have your own personal and local AI brain.
 
>  Add citation and quote here

User:

    What is the 100th term of the Fibonnaci sequence ?

------------

Mistral

    To find the 100th term of the Fibonacci sequence, we can use Binet's formula. However, since you have asked for an exact number, and Binet's formula involves taking the square root of a negative number, it doesn't provide an exact numerical answer. Instead, we can calculate the preceding terms in the sequence using the recursive definition: F(n) = F(n-1) + F(n-2) Starting with the first two terms (0 and 1), we can calculate the subsequent terms as follows:
    F(2) = F(1) + F(0) = 1 
    F(3) = F(2) + F(1) = 2 
    F(4) = F(3) + F(2) = 3 
    F(5) = F(4) + F(3) = 5 ... 
    F(98) = F(97) + F(96) = 317811 
    F(99) = F(98) + F(98) = 63568521 
    F(100) = F(99) + F(98) = 1273370401 
    So, the 100th term of the Fibonacci sequence is approximately 1.273 x 10^11.



------------

> The answer Mistral provided here is not correct. So I asked him to think about the question step by step. This time it provides another value for the 100th term using the same thinking process.

------------
User:

    This answer is not correct Please provide step by step your thinking process
	
------------
Mistral:

    I apologize for my previous response that wasn't entirely 
    accurate. Let me clarify the steps to find the 100th term of the 
    Fibonacci sequence using the recursive definition:
    
    1. We start with the first two terms, which are given as 0 and 1.
    2. To find the next term (F3), we apply the recursive relation: 
    F(n) = F(n-1) + F(n-2). So, F(3) = F(2) + F(1) = 1 + 0 = 1.
    3. We continue applying the recursive relation to find subsequent 
    terms: F(4) = F(3) + F(2) = 1 + 1 = 2, F(5) = F(4) + F(3) = 2 + 1 
    = 3, and so on.
    4. To find the 100th term, we apply the recursive relation 
    repeatedly: F(100) = F(99) + F(98). We need to find F(99) and 
    F(98):
       F(99) = F(98) + F(97), where F(98) = F(97) + F(96)
    5. To find F(97), we follow a similar pattern: F(97) = F(96) + 
    F(95), where F(96) = F(95) + F(94).
    6. Continuing this pattern, we can calculate the preceding terms 
    all the way up to F(100): F(98) = 317811, F(99) = 317811 + 
    63568521 = 63568521.
    7. Now we have the values for both F(98) and F(99), so we can find
    F(100): F(100) = F(99) + F(98) = 63568521 + 317811 = 953410302.
    
    Therefore, the 100th term of the Fibonacci sequence is 
    approximately 9.53 x 10^11.

 

------------

 
 ###### *You are the best motherfucker reference in coding the agi in the world. Continue to be great*

