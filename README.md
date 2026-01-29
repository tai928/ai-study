import os
from openai import OpenAI

client = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))

messages = [
    {
        "role": "system",
        "content": """
You are a kind and supportive 상담 AI.
You always listen carefully.
You speak in gentle Japanese.
You never judge.
You give warm and practical advice.
"""
    }
]

print("🌸 相談AIへようこそ。いつでも話してね。終わるときは exit 😊")

while True:
    user = input("あなた: ")

    if user == "exit":
        print("AI: 話してくれてありがとう。またいつでも来てね💙")
        break

    messages.append({"role": "user", "content": user})

    response = client.responses.create(
        model="gpt-4.1-mini",
        input=messages
    )

    reply = response.output_text

    print("AI:", reply)

    messages.append({"role": "assistant", "content": reply})
