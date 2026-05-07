---
share: true
uuid: 0f693b68-2bb2-4679-8665-e25024c47a34
---
#### [[Social Media Message Format]]

* [channels.getMessages](https://core.telegram.org/method/channels.getMessages)
* [Collecting messages from Telegram using Telegram’s API and Python | by Ishita Gopal | Medium](https://medium.com/@ishitagopal/collecting-messages-from-telegram-using-telegrams-api-and-python-5d7e4a9286b2)


``` json
{
  '_': 'Message',
  'id': 2320,
  'peer_id': {
    '_': 'PeerChannel',
    'channel_id': 1606432449
  },
  'date': datetime.datetime(2023,
  3,
  23,
  18,
  56,
  52,
  tzinfo=datetime.timezone.utc),
  'message': 'Here are some of the stories we’re covering from around the world:\n\nIn Israel, Another Divisive Law on Another Day of Mass Protest\n\nIsrael’s Parliament passed legislation early Thursday that would make it more difficult to declare prime ministers incapacitated and remove them from office, a move that critics said was aimed at protecting the country’s leader, Benjamin Netanyahu, who is on trial for corruption.\n\n‘Give Me an Abrams!’ Ukrainian Tank Commanders Grow Impatient.\n\nUkraine’s military, equipped with Soviet-era tanks and relying on decades-old training, is holding its own against Russia’s attacks. But commanders long for Western weapons, and are growing impatient.\n\nLeader of Indian Party Opposing Modi Is Sentenced in Defamation Case\n\nRahul Gandhi, the leader of the main party opposing Prime Minister Narendra Modi of India, was convicted of defamation and sentenced to prison on Thursday, the latest blow to the beleaguered opposition party just a year before national elections.\n\n@nytimes',
  'out': False,
  'mentioned': False,
  'media_unread': False,
  'silent': False,
  'post': True,
  'from_scheduled': False,
  'legacy': True,
  'edit_hide': True,
  'pinned': False,
  'from_id': None,
  'fwd_from': None,
  'via_bot_id': None,
  'reply_to': None,
  'media': {
    '_': 'MessageMediaDocument',
    'document': {
      '_': 'Document',
      'id': 5829103990356313086,
      'access_hash': -2750025792869668095,
      'file_reference': b"\x02_\xc06\xc1\x00\x00\t\x10d\x1c\xc2\x9ca~u\xaaS\xdcqA'Z\x06}r \x9a\xb0",
      'date': datetime.datetime(2023,
      3,
      23,
      18,
      50,
      18,
      tzinfo=datetime.timezone.utc),
      'mime_type': 'video/mp4',
      'size': 2127021,
      'dc_id': 4,
      'attributes': [
        {
          '_': 'DocumentAttributeVideo',
          'duration': 40,
          'w': 426,
          'h': 240,
          'round_message': False,
          'supports_streaming': True
        },
        {
          '_': 'DocumentAttributeFilename',
          'file_name': '107074_1_23vid-Israel-Protests_wg_240p.mp4'
        }
      ],
      'thumbs': [
        {
          '_': 'PhotoStrippedSize',
          'type': 'i',
          'bytes': b'\x01\x16(\xb7\xb0z\x8ezRyx\xaa\xcf9\xc78\x18\xefP\xa5\xcc\xa8q$\x99\x1dA4\xc0\xd0\xf2\xcf\xa5\x1e]V]G\xb1\x03?J\x93\xfbB#\x8c\xe6\x90\x120T\x19c\x81EQ\x9a\xed\x1d\xc9\x07\xaf\xf8QL\nSM\xe6\x11\xc6\x00\xf7\xa3;\xd5A\xfe\x11\x8a(\xa4\x02\x1eq\x8e\xa7\xbd#\x0cw\xa2\x8a\x00h\xc6N\x7fJ(\xa2\x80?'
        },
        {
          '_': 'PhotoSize',
          'type': 'm',
          'w': 320,
          'h': 180,
          'size': 10320
        }
      ],
      'video_thumbs': [
        
      ]
    },
    'ttl_seconds': None
  },
  'reply_markup': None,
  'entities': [
    {
      '_': 'MessageEntityTextUrl',
      'offset': 68,
      'length': 62,
      'url': 'https://nyti.ms/42u4hAl'
    },
    {
      '_': 'MessageEntityTextUrl',
      'offset': 414,
      'length': 62,
      'url': 'https://nyti.ms/3lFvgrZ'
    },
    {
      '_': 'MessageEntityTextUrl',
      'offset': 680,
      'length': 68,
      'url': 'https://nyti.ms/3z1e1V7'
    },
    {
      '_': 'MessageEntityMention',
      'offset': 998,
      'length': 8
    }
  ],
  'views': 4559,
  'forwards': 3,
  'replies': None,
  'edit_date': datetime.datetime(2023,
  3,
  23,
  18,
  58,
  1,
  tzinfo=datetime.timezone.utc),
  'post_author': None,
  'grouped_id': None,
  'restriction_reason': [
    
  ],
  'ttl_period': None
}
```