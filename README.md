- 👋 Hi, I’m @UDDABBhakta
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
- 📱 WhatsApp number: 8001019102

<!---
UDDABBhakta/UDDABBhakta is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
const { spawnSync } = require('child_process')
const { existsSync, writeFileSync } = require('fs')

const SESSION_ID = 'updateThis' // Edit this line only, don't remove ' <- this symbol

if (!existsSync('levanter')) {
  process.env.COREPACK_ENABLE=0

  console.log('Cloning the repository...')
  const cloneResult = spawnSync(
    'git',
    ['clone', 'https://github.com/lyfe00011/levanter.git', 'levanter'],
    {
      stdio: 'inherit',
    }
  )

  if (cloneResult.error) {
    throw new Error(`Failed to clone the repository: ${cloneResult.error.message}`)
  }

  const configPath = 'levanter/config.env'
  try {
    console.log('Writing to config.env...')
    writeFileSync(configPath, `VPS=true\nSESSION_ID=${SESSION_ID}`)
  } catch (err) {
    throw new Error(`Failed to write to config.env: ${err.message}`)
  }

  console.log('Installing dependencies...')
  const installResult = spawnSync('yarn', ['install', '--network-concurrency', '3'], {
    cwd: 'levanter',
    stdio: 'inherit',
  })

  if (installResult.error) {
    throw new Error(`Failed to install dependencies: ${installResult.error.message}`)
  }
}
spawnSync('yarn', ['start'], { cwd: 'levanter', stdio: 'inherit' })
