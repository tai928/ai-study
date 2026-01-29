import os
from openai import OpenAI

client = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))

messages = [
    {"role": "system", "content": "You are a friendly assistant who talks politely in Japanese."}
]

print("AIと会話できます。終わるときは exit と入力してね😊")

while True:
    user = input("あなた: ")

    if user == "exit":
        print("AI: またね！")
        break

    messages.append({"role": "user", "content": user})

    response = client.responses.create(
        model="gpt-4.1-mini",
        input=messages
    )

    ai_reply = response.output_text

    print("AI:", ai_reply)

    messages.append({"role": "assistant", "content": ai_reply})
