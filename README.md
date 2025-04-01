# UGV
ugv

# ctrl signal
# single-ended vs differential input
the project use: 
  single-endded : multipul inputs are all connected to one ground
# set all the input pin to enable Continuous Mode
   for multiple input 
   DMA(direct memory access) method
   start to convert the onput as long as the previous conversion is done

   #include <stdio.h>
#include <string.h>
#include "api.h"

uint8_t pk[CRYPTO_PUBLICKEYBYTES];
uint8_t sk[CRYPTO_SECRETKEYBYTES];
uint8_t sig[CRYPTO_BYTES];
uint8_t msg[] = "rainy day: lattice beam armed";
size_t siglen;

int main() {
    init_platform();
    xil_printf("🔐 Quantum Rain is Falling 🌧️\n");

    crypto_sign_keypair(pk, sk);
    xil_printf("Keypair generated.\n");

    crypto_sign_signature(sig, &siglen, msg, strlen((char *)msg), sk);
    xil_printf("Message signed. Sig length: %d\n", siglen);

    int status = crypto_sign_verify(sig, siglen, msg, strlen((char *)msg), pk);

    if (status == 0) {
        xil_printf("✅ Signature is VALID!\n");
    } else {
        xil_printf("❌ Signature is INVALID!\n");
    }

    while (1);  // Keep running
    return 0;
}
   
   

