---
title: Wenming
comments: true
published: true
tags: history

---

## Wenming Area

```text
        private CCSafeNotificationCenter() { }

        ~CCSafeNotificationCenter()
        {
            foreach (var item in this.m_observers)
            {
                foreach (var i in item.Value)
                    i.Value.release();
            }
            this.m_observers.Clear();
        }

```
